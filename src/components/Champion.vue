<template>
  <div id="champion">
    <br>
    <div class="avatar">
    <img :src="'/img/champion/tiles/' + selected + '_0.jpg'">
    </div>
    <div id="mainselect">
      <select v-model="selected">
        <option disabled value>Select a champion</option>
        <option v-for="champion in champions" v-bind:value="champion.name">{{ champion.name }}</option>
      </select>
    </div>
    
    <span>
      Level
      <h5>{{ level }}</h5>

      <button @click="increaseCounter(18)" class="button rounded shadow success">+</button>
      <!-- Decrease Counter, with an `decreaseLimit` of 0 -->
      <button @click="decreaseCounter(1)" class="button rounded shadow warning">-</button>
    </span>
    <span>{{ selected }}</span>
    
    <!-- <img :src="require(`imgName(selected)`)" alt="">
    -->
   
    <div class="json">{{ entity }}</div>

    <div class="btn hp">
      <span>Base HP</span>
      {{ entity["hp"] + ((level - 1) * entity["hpperlevel"]) }}
    </div>
    <div class="btn hpregen">
      <span>BASE HPREGEN</span>
      {{ entity["hpregen"] + (entity["hpregenperlevel"] * level) }}
    </div>
    <div class="btn hp">
      <span>BASE ARMOR</span>
      {{ entity["armor"] + (entity["armorperlevel"] * level) }}
    </div>

    <div class="btn spellblock">
      <span>BASE MR</span>
      {{ entity["spellblock"] + (entity["spellblockperlevel"] * level) }}
    </div>
    <div class="btn mp">
      <span>BASE MP</span>
      {{ entity["mp"] + (entity["mpperlevel"] * level) }}
    </div>
    <div class="btn mpregen">
      <span>BASE MPREGEN</span>
      {{ entity["mpregen"] + (entity["mpregenperlevel"] * level) }}
    </div>
    <div class="btn attackdamage">
      <span>AD</span>
      <br>
      <span>Bonus AD</span>
      <br>
      <span>Base AD</span>
      {{ entity["attackdamage"] + (entity["attackdamageperlevel"] * level) }}
      <br>
      <span>Crit chance</span>
      {{ entity["crit"] }}
    </div>

    <div class="pens">
      <div class="letality">
        <span>Letality</span>
        <span>{{letality}}</span>
        <br>
        <span>Armor Penetration</span>
        <span>{{ armpen }}</span>
      </div>
      <div class="magpen">
        <span>Magic Penetration</span>
        <span>{{ magpen }}</span>
        <br>
        <span>Flat Magic Penetration</span>
        <span>{{ magpen }}</span>
      </div>
    </div>
    <div class="abilitypower">
      <div class="AP">
        <span>Ability Power</span>
        <span>{{AP}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bonusArmor: 0,
      entity: "",
      level: 1,
      AP: 0,
      letality: 0,
      magpen: 0,
      armpen: 0,
      bonusHp: 0,
      entityTotalHp: 0,
      champions: [
        { id: 0, name: "Camille" },
        { id: 1, name: "Vayne" },
        { id: 3, name: "Janna" },
        { id: 4, name: "Shyvana" },
        { id: 5, name: "Shen" }
      ],
      selected: ""
    };
  },
  methods: {
    increaseCounter(increaseLimit) {
      // Increase
      if (this.level < increaseLimit) this.level++;
    },
    decreaseCounter(decreaseLimit) {
      // Decrease
      if (this.level > decreaseLimit) this.level--;
    },
    imgName: function(selected) {
      if (selected === "") {
        return "https://bestapples.com/wp-content/uploads/2015/10/apple-varieties.jpg";
      } else {
        var imgPath = "src/img/champion/tiles/" + selected + "_0.jpg";
        return imgPath;
      }
    }
  },
  watch: {
    selected: function(newSelected) {
      console.log(`watch triggered, value of selected is: ${newSelected}`);
      axios
        .get("../champion.json")
        .then(
          response =>
            (this.entity = response.data.data[`${newSelected}`]["stats"])
        );
    },
    level: function(newLevel) {
      console.log(`watch triggered. New level is ${newLevel}`);
    }
  }
};
</script>
<style scoped>
* {
  box-sizing: border-box;
}
#champion {
  font-family: Helvetica;
  font-size: 0.75em;
  max-width: 800px;
  margin: 30px auto;
  padding: 0 20px;
  width: 100%;
  /* display: grid !important;
  /* Define Auto Row size */
  /* grid-auto-rows: 100px; */
  /*Define our columns */
  /* grid-template-columns: 120px 120px; */
  /* grid-gap: 1em; */ 
}

.btn {
  border-radius: 10px;
  padding: 20px;
  color: #fff;
  max-width: 320px;
}

.btn:nth-child(odd) {
  background-color: darkolivegreen;
}

.btn:nth-child(even) {
  background-color: purple;
}
.json {
  display: none;
}
</style>