<template>
  <div class="inventory">
    <h3>Exclude URLs</h3>
    <ul class="pattern">
      <h4>Exclude Pattern</h4>
      <div>Count: {{ ExcludePattern.length }}</div>
      <div v-for="(pattern, index) in ExcludePattern" :key="pattern.id">
        <li>
          <div class="container">
            <input type="radio" :id="'excludeUrlPatternCheckID'+index" name="excludeUrlPattern" :value="pattern.excludeUrlPattern" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" :for="'excludeUrlPatternCheckID'+index" :key="'label' + pattern">
              Pattern {{ index + 1 }}
              <br>{{ pattern.excludeUrlPattern }}
            </label>
          </div>
        </li>
      </div>
      <div>
      <li>
        <div class="container">
            <input type="radio" id="excludeEmpty" name="excludeUrlPattern" value="" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" for="excludeEmpty">
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
  name: 'InventoryExcludeSection',
  props: {
    ExcludePattern: Array
  },
  data () {
    return {
      selected: false
    }
  },
  methods: {
    uncheck (pattern) {
      if (pattern === this.selected) {
        this.selected = false
      } else {
        this.selected = pattern
      }
    }
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
