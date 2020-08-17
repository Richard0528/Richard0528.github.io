<template>
  <div class="inventory-detail">
    <h3>Inverntory Details</h3>
    <ul class="pattern">
      <h4>Vin Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesVinPatternsReturn.length }}</div>
      <div v-for="(vinpattern, index) in DetailJson.getDMSModelInventoriesVinPatternsReturn" :key="vinpattern.id">
        <li>
          <div class="container">
            <input type="radio" :key="'input' + vinpattern" :id="'vinPatternCheckID'+index" name="vinPattern" :value="vinpattern.vinPattern" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" :for="'vinPatternCheckID'+index" :key="'label' + vinpattern">
                Vin Pattern {{ index + 1 }}
              <br>{{ vinpattern.vin }}
              <br>{{ vinpattern.vinPattern }}
            </label>
          </div>
        </li>
      </div>
      <div>
        <li>
        <div class="container">
          <input type="radio" id="vinEmpty" name="vinPattern" value="" checked="checked" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="radioLabel" for="vinEmpty">
            null
          </label>
        </div>
      </li>
      </div>
    </ul>
    <ul class="pattern">
      <h4>Color Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesColorPatternsReturn.length }}</div>
      <div v-for="(colorpattern, index) in DetailJson.getDMSModelInventoriesColorPatternsReturn" :key="colorpattern.id">
        <li>
          <div class="container">
            <input type="radio" :key="'input' + colorpattern" :id="'colorPatternCheckID'+index" name="colorPattern" :value="colorpattern.colorPattern" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" :for="'colorPatternCheckID'+index" :key="'label' + colorpattern">
              Color Pattern {{ index + 1 }}
              <br>{{ colorpattern.color }}
              <br>{{ colorpattern.colorPattern }}
            </label>
          </div>
        </li>
      </div>
      <div>
        <li>
          <div class="container">
            <input type="radio" id="colorEmpty" name="colorPattern" value="" checked="checked" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" for="colorEmpty">
              null
            </label>
          </div>
        </li>
      </div>
    </ul>
    <ul class="pattern">
      <h4>Mileage Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesMileagePatternsReturn.length }}</div>
      <div v-for="(mileagepattern, index) in DetailJson.getDMSModelInventoriesMileagePatternsReturn" :key="mileagepattern.id">
        <li>
          <div class="container">
            <input type="radio" :key="'input' + mileagepattern" :id="'mileagePatternCheckID'+index" name="mileagePattern" :value="mileagepattern.mileagePattern" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" :for="'mileagePatternCheckID'+index" :key="'label' + mileagepattern">
              Mileage Pattern {{ index + 1 }}
              <br>{{ mileagepattern.mileage }}
              <br>{{ mileagepattern.mileagePattern }}
            </label>
          </div>
        </li>
      </div>
      <div>
        <li>
          <div class="container">
            <input type="radio" id="mileageEmpty" name="mileagePattern" value="" checked="checked" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" for="mileageEmpty">
              null
            </label>
          </div>
        </li>
      </div>
    </ul>
    <ul class="pattern">
      <h4>Price Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesPricePatternsReturn.length }}</div>
      <div v-for="(pricepattern, index) in DetailJson.getDMSModelInventoriesPricePatternsReturn" :key="pricepattern.id">
        <li>
          <div class="container">
            <input type="radio" :key="'input' + pricepattern" :id="'pricePatternCheckID'+index" name="pricePattern" :value="pricepattern.pricePattern" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" :for="'pricePatternCheckID'+index" :key="'label' + pricepattern">
              Price Pattern {{ index + 1 }}
              <br>{{ pricepattern.price }}
              <br>{{ pricepattern.pricePattern }}
            </label>
          </div>
        </li>
      </div>
      <div>
        <li>
          <div class="container">
            <input type="radio" id="priceEmpty" name="pricePattern" value="" checked="checked" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" for="priceEmpty">
              null
            </label>
          </div>
        </li>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'InventoryDetailSection',
  props: {
    DetailJson: Object
  },
  data () {
    return {
    }
  },
  methods: {
  },
  watch: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul > li {
  display: inline-block;
  margin: 10px 30px;
  *display: inline;
}
.container {
  margin: auto;
  max-width: 1000px;
}
input[type = "radio"]:checked + label {
  color: red;
  font-weight: bold;
}
input[type = "radio"] {
  display: none;
}
.radioLabel:hover {
  padding: 0px 0px 0px 5px;
  cursor: pointer;
}
ul.pattern {
  list-style-type: none;
}
</style>
