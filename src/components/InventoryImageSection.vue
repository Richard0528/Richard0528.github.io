<template>
  <div class="inventory">
    <h3>Image URLs</h3>
    <ul class="pattern">
        <h4>Image Pattern</h4>
        <div>Count: {{ ImagePattern.length }}</div>
        <div v-for="(pattern, index) in ImagePattern" :key="pattern.id">
          <li>
            <div class="container">
              <input type="radio" :id="'ImagePatternCheckID'+index" name="imageUrlPattern" :value="pattern.imageUrlPattern" @change="$emit('wanted_url_pattern', $event.target)">
              <label class="radioLabel" :for="'ImagePatternCheckID'+index" :key="'label' + pattern">
                Pattern {{ index + 1 }}
                <br>Count: {{ pattern.urlCount }}
                <div class="row">
                  <p>
                    <button class="btn btn-info" type="button" data-toggle="collapse" :data-target="'#ImagePatternCollapse'+index" aria-expanded="false" :aria-controls="'ImagePatternCollapse'+index">
                      Example #{{index + 1}}
                    </button>
                  </p>
                  <div class="collapse" :id="'ImagePatternCollapse'+index">
                    <div class="card card-body">
                      <div v-for="(sample, index) in pattern.imageUrl" :key="index">
                            {{ sample }}
                      </div>
                    </div>
                  </div>
                </div>
              </label>
            </div>
          </li>
        </div>
      <div>
        <li>
          <div class="container">
            <input type="radio" id="imageEmpty" name="imageUrlPattern" value="" @change="$emit('wanted_url_pattern', $event.target)">
            <label class="radioLabel" for="imageEmpty">
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
  name: 'InventoryImageSection',
  props: {
    ImagePattern: Array
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
