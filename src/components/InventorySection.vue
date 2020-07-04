<template>
  <div class="inventory">
    <h3>Inverntory URLs</h3>
    <ul>
      <h4>URL Pattern</h4>
      <div>Count: {{ UrlPattern.length }}</div>
      <li v-for="(pattern, index) in UrlPattern" :key="pattern.patternID">
        <div class="container">
          <input type="checkbox" :id="'UrlPatternCheckID'+index" name="urlPattern" :value="pattern.matchedUrlPattern" @change="$emit('wanted_url_pattern', 'urlPattern', modified(pattern.matchedUrlPattern))">
          <label class="checkboxLabel" :for="'UrlPatternCheckID'+index">
            Pattern {{ index + 1 }}
            <br>Count: {{ pattern.matchedUrlCount }}
            <div class="row">
              <p>
                <button class="btn btn-info" type="button" data-toggle="collapse" :data-target="'#UrlPatternCollapse'+index" aria-expanded="false" :aria-controls="'UrlPatternCollapse'+index">
                  Example #{{index + 1}}
                </button>
              </p>
              <div class="collapse" :id="'UrlPatternCollapse'+index">
                <div class="card card-body">
                  <div v-for="(sample, index) in pattern.samplesUrl" :key="index">
                        {{ sample }}
                  </div>
                </div>
              </div>
            </div>
          </label>
        </div>
      </li>
    </ul>
    <ul>
      <h4>Next Page Pattern</h4>
      <div>Count: {{ UrlNextPagePattern.length }}</div>
      <li v-for="(pattern, index) in UrlNextPagePattern" :key="pattern.id">
        <div class="container">
          <input type="checkbox" :id="'nextPagePatternCheckID'+index" name="nextPagePattern" :value="pattern.nextPagePattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'nextPagePatternCheckID'+index">
            Pattern {{ index + 1 }}
            <br>{{ pattern.nextPagePattern }}
          </label>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'InventorySection',
  props: {
    UrlPattern: Array,
    UrlNextPagePattern: Array
  },
  data () {
    return {
    }
  },
  methods: {
    modified (str) {
      console.log('in modified')
      console.log(str)
      return str.replace(/\\/g, '\\')
    }
  },
  watch: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul > li {
  display: block;
  margin: 10px 30px;
}
.container {
  margin: auto;
  max-width: 1000px;
}
input[type = "checkbox"]:checked + label {
  color: red;
  font-weight: bold;
}
input[type = "checkbox"] {
  display: none;
}
.checkboxLabel:hover {
  padding: 0px 0px 0px 5px;
  cursor: pointer;
}
</style>
