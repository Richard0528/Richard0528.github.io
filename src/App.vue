<template>
  <div class="container" id="app">
    <div class="row">
      <div class="card h-100 px-0 border-primary col-sm-3">
        <div class="card-body">
          <h5 class="card-title">Pattern</h5>
          <div v-for="(value, name) in finalList" :key="name">
            {{ name }} : {{ value }}
          </div>
          <br>
          <button type="button" class="btn btn-success" @click="insertToDB">Submit</button>
        </div>
      </div>
      <div class="container col-sm-9">
        <h2 style="text-align: center;">Group Patterns System</h2>
        <br>
        <br>
        <div class="input-group mb-3">
          <input type="text" style="width: 40%;" class="input-text" placeholder="Please enter a URL" v-model.lazy="userInputURL">
          <input type="text" style="width: 15%;" class="input-text" placeholder="# of demo model" v-model.lazy="userInputModelNum">
          <button type="button" class="btn btn-primary" @click="retrieveFromURL">Search</button>
        </div>
        <InventorySection v-if="urlPattern.length" :UrlPattern="urlPattern" :UrlNextPagePattern="nextPagePattern"
                          @wanted_url_pattern="test"/>
        <hr>
        <InventoryDetailSection v-if="detailJson !== ''" :DetailJson="detailJson" @wanted_url_pattern="addToPatternList"/>
        <hr>
        <InventoryImageSection v-if="imagePattern.length" :ImagePattern="imagePattern" @wanted_url_pattern="addToPatternList"/>
        <hr>
        <InventoryExcludeSection v-if="excludePattern.length" :ExcludePattern="excludePattern" @wanted_url_pattern="addToPatternList"/>
        <hr>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import InventorySection from './components/InventorySection.vue'
import InventoryDetailSection from './components/InventoryDetailSection.vue'
import InventoryImageSection from './components/InventoryImageSection.vue'
import InventoryExcludeSection from './components/InventoryExcludeSection.vue'

export default {
  name: 'App',
  components: {
    InventorySection,
    InventoryDetailSection,
    InventoryImageSection,
    InventoryExcludeSection
  },
  data () {
    return {
      userInputURL: '',
      userInputModelNum: 1,
      resultJson: '',
      // Inventory URL
      urlPattern: [],
      nextPagePattern: [],
      // Inventory Detail
      detailJson: '',
      // image url
      imagePattern: [],
      // exclude url
      excludePattern: [],
      // final dict to collect all the user picked pattern
      // initialize this dict with a method
      finalList: this.initialFinalList()
    }
  },
  methods: {
    initialFinalList () {
      return {
        businessID: this.userInputURL,
        inventoryUrl: [],
        urlPattern: [],
        nextPagePattern: [],
        vinPattern: [],
        colorPattern: [],
        mileagePattern: [],
        pricePattern: [],
        imageUrlPattern: [],
        excludeUrlPattern: []
      }
    },
    async retrieveFromURL () {
      if (this.userInputURL === '') {
        return
      }
      this.finalList = this.initialFinalList()
      try {
        const result = await axios({
          method: 'POST',
          url: 'http://54.191.215.56:8191/graphql',
          data: {
            query: `
              query GetGroupMatchPatterns {
                getGroupMatchPatterns(
                  demoModel: ` + this.userInputModelNum + `,
                  businessID: "` + this.userInputURL + `", 
                  chromeAndWebDriverVersion: "chrome79"
                ) {
                  domain
                  inventoryUrl
                  detailsPageUrl
                  getDMSModelInventoriesUrlServiceReturn {
                    patternID
                    matchedUrlPattern
                    matchedUrlCount
                    samplesUrl
                  }
                  getDMSModelInventoriesNextPagePatternsReturn {
                    id
                    dmsId
                    nextPagePattern
                  }
                  getDMSInventoriesDetailsReturn {
                    getDMSModelInventoriesVinPatternsReturn {
                      id
                      dmsId
                      vin
                      vinPattern
                    }
                    getDMSModelInventoriesColorPatternsReturn {
                      id
                      dmsId
                      color
                      colorPattern
                    }
                    getDMSModelInventoriesMileagePatternsReturn {
                      id
                      dmsId
                      mileage
                      mileagePattern
                    }
                    getDMSModelInventoriesPricePatternsReturn {
                      id
                      dmsId
                      price
                      pricePattern
                    }
                  }
                  getDMSModelInventoriesImageUrlReturn {
                    id
                    dmsId
                    imageUrlPattern
                    urlCount
                    imageUrl
                  }
                  getDmsModelInventoriesExcludeUrlReturn {
                    id
                    dmsId
                    excludeUrlPattern
                  }
                }
              }
            `
          }
        })
        // Inventory URL
        const resultJson = result.data.data.getGroupMatchPatterns
        console.log(result.data)
        // assign value of inventory Url that user requested
        this.finalList.inventoryUrl = resultJson.inventoryUrl
        // Service URL and Next Page
        this.urlPattern = resultJson.getDMSModelInventoriesUrlServiceReturn
        this.nextPagePattern = resultJson.getDMSModelInventoriesNextPagePatternsReturn
        // Inventory Detail
        this.detailJson = resultJson.getDMSInventoriesDetailsReturn
        // image url
        this.imagePattern = resultJson.getDMSModelInventoriesImageUrlReturn
        // exclude url
        this.excludePattern = resultJson.getDmsModelInventoriesExcludeUrlReturn
      } catch (error) {
        console.error(error)
      }
    },
    addToPatternList (checkbox) {
      const wantedPattern = checkbox.value
      console.log(checkbox)
      const patternType = checkbox.name
      if (checkbox.checked) {
        if (!this.finalList[patternType].includes(wantedPattern)) {
          this.finalList[patternType].push(wantedPattern)
        }
      } else {
        this.finalList[patternType] = this.finalList[patternType].filter(pattern => {
          return pattern !== wantedPattern
        })
      }
    },
    test (a, b) {
      console.log(a)
      console.log(b)
    },
    async insertToDB () {
      try {
        const result = await axios({
          method: 'POST',
          url: 'http://54.191.215.56:8191/graphql',
          data: {
            query: `
              mutation SetGroupMatchPatterns {
                setGroupMatchPatterns(
                  businessID: "` + this.userInputURL + `",
                  inventoryUrl: "` + this.finalList.inventoryUrl + `",
                  urlPattern: "` + this.finalList.urlPattern + `",
                  nextPagePattern: "` + this.finalList.nextPagePattern + `",
                  vinPattern: "` + this.finalList.vinPattern + `",
                  colorPattern: "` + this.finalList.colorPattern + `",
                  mileagePattern: "` + this.finalList.mileagePattern + `",
                  pricePattern: "` + this.finalList.pricePattern + `",
                  imageUrlPattern: "` + this.finalList.imageUrlPattern + `",
                  excludeUrlPattern: "` + this.finalList.excludeUrlPattern + `"
                )
              }
            `
          }
        })
        const resultJson = result.data
        console.log(resultJson)
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.input-group {
  margin: 0px 15%;
}

.input-text {
  border-radius: 8px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  border: none;
  margin-right: 2.5%;
  padding: .6rem .75rem;
}

.input-text:focus {
  outline: none;
  box-shadow: 0px 0px 5px rgba(44, 204, 195, 0.8);
}

.btn-primary, .btn-primary:hover, .btn-primary:active, .btn-primary:visited {
  background-color: #24A49C;
  width: 15%;
  border-radius: 10px;
  font-size: larger;
}

.btn-success, .btn-success:hover, .btn-success:active, .btn-success:visited {
  background-color: #24A49C;
  border-radius: 10px;
}

</style>
