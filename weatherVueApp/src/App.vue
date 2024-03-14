<script>
import axios from "axios";

export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },
  computed: {
    cityName() {
      return "'" + this.city + "'";
    },
    showTemp() {
      return "Temperature " + this.info.main.temp;
    },
    showFeelsLike() {
      return "Feels like " + this.info.main.feels_like;
    },
    showMinTemp() {
      return "Temperature min " + this.info.main.temp_min;
    },
    showMaxTemp() {
      return "Temperature max " + this.info.main.temp_max;
    },
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Need the name of more than one symbol :)";
        return false;
      }
      this.error = "";
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=01e9ec61492059647d9339c849ff267c`
        )
        .then((res) => (this.info = res.data));
    },
  },
};
</script>

<template>
  <div className="wrapper">
    <h1>Weather App</h1>
    <p>Find out the weather in {{ city === "" ? "in your city" : cityName }}</p>
    <input
      type="text"
      v-model="city"
      @input="this.city = $event.target.value"
      placeholder="City"
    />
    <button @click="getWeather()" v-if="city !== ''">Get weather</button>
    <button disabled v-else="city !== ''">Enter the name of the city</button>
    <p className="error">{{ error }}</p>
    <div v-if="info !== null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: #d03939;
}
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: #19254b;
  padding-top: 50px;
  text-align: center;
}

.wrapper p {
  margin-top: 20px;
}
.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #ffffff;
  padding: 5px 15px;
  font-size: 14px;
  outline: none;
  color: white;
}
.wrapper input:focus {
  border-bottom-color: green;
}
.wrapper button {
  padding: 5px 10px;
  border-radius: 10px;
  border: none;
  background-color: #dfa63b;
  cursor: pointer;
  margin-left: 10px;
}
.wrapper button:active {
  transform: translateY(-2px);
}
.wrapper button:disabled {
  color: black;
  background-color: #2aa88d;
}
</style>
