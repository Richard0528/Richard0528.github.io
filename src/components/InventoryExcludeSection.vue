<template>
  <div class="inventory">
    <h3>Exclude URLs</h3>
    <ul>
      <h4>Exclude Pattern</h4>
      <div>Count: {{ ExcludePattern.length }}</div>
      <li v-for="(pattern, index) in ExcludePattern" :key="pattern.id">
        <div class="container">
          <input type="checkbox" :id="'excludeUrlPatternCheckID'+index" name="excludeUrlPattern" :value="pattern.excludeUrlPattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'excludeUrlPatternCheckID'+index">
            Pattern {{ index + 1 }}
            <br>{{ pattern.excludeUrlPattern }}
          </label>
        </div>
      </li>
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
