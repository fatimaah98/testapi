<template>
 <div class="app">
    <select name="" id="" @change="selectCity">
      <option value="" >select city </option>
      <option :value="city.id" v-for="(city,i) in cityArray" :key="i">
        {{city.title}}
      </option>
    </select>
    <select name="" id="">
      <option value="">select town </option>
      <option value="" v-for="(town,i) in townShips" :key="i">{{town.title}}</option>
    </select>
 </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      cityUrl: "https://reservam.iran.liara.run/v1/city",
      cityArray:null,
      citySelected:'',
      townShips:null,
    }
  },

  mounted() {
    axios.get(this.cityUrl)
    .then(response => {
      this.cityArray = response.data.data;
    })
    .catch(error => {
      console.log(error);
    })
  },

  methods: {
    selectCity(e) {
      this.cityArray.forEach(city => {
          if(city.id == e.target.value) this.townShips = city.Townships;
          else return
      });
    }
  },
}
</script>

<style>

</style>
