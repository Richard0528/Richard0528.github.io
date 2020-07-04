<template>
  <div class="inventory-detail">
    <h3>Inverntory Details</h3>
    <ul>
      <h4>Vin Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesVinPatternsReturn.length }}</div>
      <li v-for="(vinpattern, index) in DetailJson.getDMSModelInventoriesVinPatternsReturn" :key="vinpattern.id">
        <div class="container">
          <input type="checkbox" :id="'vinPatternCheckID'+index" name="vinPattern" :value="vinpattern.vinPattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'vinPatternCheckID'+index">
            Vin Pattern {{ index + 1 }}
            <br>{{ vinpattern.vin }}
            <br>{{ vinpattern.vinPattern }}
          </label>
        </div>
      </li>
    </ul>
    <ul>
      <h4>Color Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesColorPatternsReturn.length }}</div>
      <li v-for="(colorpattern, index) in DetailJson.getDMSModelInventoriesColorPatternsReturn" :key="colorpattern.id">
        <div class="container">
          <input type="checkbox" :id="'colorPatternCheckID'+index" name="colorPattern" :value="colorpattern.colorPattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'colorPatternCheckID'+index">
            Color Pattern {{ index + 1 }}
            <br>{{ colorpattern.color }}
            <br>{{ colorpattern.colorPattern }}
          </label>
        </div>
      </li>
    </ul>
    <ul>
      <h4>Mileage Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesMileagePatternsReturn.length }}</div>
      <li v-for="(mileagepattern, index) in DetailJson.getDMSModelInventoriesMileagePatternsReturn" :key="mileagepattern.id">
        <div class="container">
          <input type="checkbox" :id="'mileagePatternCheckID'+index" name="mileagePattern" :value="mileagepattern.mileagePattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'mileagePatternCheckID'+index">
            Mileage Pattern {{ index + 1 }}
            <br>{{ mileagepattern.mileage }}
            <br>{{ mileagepattern.mileagePattern }}
          </label>
        </div>
      </li>
    </ul>
    <ul>
      <h4>Price Pattern</h4>
      <div>Count: {{ DetailJson.getDMSModelInventoriesPricePatternsReturn.length }}</div>
      <li v-for="(pricepattern, index) in DetailJson.getDMSModelInventoriesPricePatternsReturn" :key="pricepattern.id">
        <div class="container">
          <input type="checkbox" :id="'pricePatternCheckID'+index" name="pricePattern" :value="pricepattern.pricePattern" @change="$emit('wanted_url_pattern', $event.target)">
          <label class="checkboxLabel" :for="'pricePatternCheckID'+index">
            Price Pattern {{ index + 1 }}
            <br>{{ pricepattern.price }}
            <br>{{ pricepattern.pricePattern }}
          </label>
        </div>
      </li>
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
