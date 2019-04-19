<template>
  <div id="drake">
    <div>
      <h3>DRAKE</h3>

      <div>Select drake</div>
      <div>+</div>
      <select v-model="selected">
        <option disabled value="">Select drake</option>
        <option v-for="option in options" v-bind:name="option.name">
          {{ option.name }}
        </option>
      </select>
      <span>Selected: {{ selected }}</span>
      <a class="button is-danger" @click.prevent="incrementCounter">+</a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
      selected: "Add Drake",
      options: [
        { id: 0, name: "Infernal" },
        { id: 1, name: "Montain" },
        { id: 2, name: "Cloud" },
        { id: 3, name: "Ocean" },
        { id: 3, name: "Elder" }
      ]
    };
  },
  methods: {
    incrementCounter: function() {
      this.drakeLevelCount += 1;
      if (this.drakeLevelCount <= 0 || this.drakeLevelCount > 3) {
        alert("А вот..");
        alert("..и неправильно!");
        this.drakeLevelCount;
      }
    }
  }
};
</script>

<style scoped>
#drake {
  font-family: Helvetica;
  font-size: 0.75em;
  max-width: 800px;
  margin: 30px auto;
  padding: 0 20px;
  width: 100%;
  display: grid !important;
  /* Define Auto Row size */
  grid-auto-rows: 100px;
  /*Define our columns */
  grid-template-columns: repeat(auto-fill, minmax(200px, 0.5fr));
  grid-gap: 1em;
  margin-top: 60px;
  border-style: solid;
  border-color: rebeccapurple;
}
</style>
