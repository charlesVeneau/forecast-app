<template>
  <div class="home">
    <div class="input-container">
      <input
        type="text"
        placeholder="Entrez une ville"
        class="input"
        v-model="citySearchString"
        @input="debounceForecast()"
      />
    </div>
    <div class="cards">
      <Card v-if="forecast" :forecast="forecast" />
      <div v-else class="errorMsg">City not found!</div>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card.vue";
import axios from "axios";
import _ from "lodash";

export default {
  components: {
    Card
  },
  data() {
    return {
      citySearchString: "",
      forecast: null
    };
  },
  created() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/weather?q=paris,fr&appid=${process.env.VUE_APP_OPENWEATHER}&units=metric&lang=fr`
      )
      .then(res => {
        this.forecast = res.data;
      });
  },
  methods: {
    debounceForecast: _.debounce(function(){
      this.getForecast()
    }, 600),
    getForecast() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.citySearchString}&appid=${process.env.VUE_APP_OPENWEATHER}&units=metric&lang=fr`
        )
        .then(res => {
          this.forecast = res.data;
        })
        .catch(e => console.log(e), (this.forecast = null));
    },
  
  }
};
</script>
