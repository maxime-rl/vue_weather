<template>
  <div class="container">
    <div class="row">
      <div class="col-12 d-flex justify-content-center">
        <div class="card" style="width: 18rem;">
          <div class="card-body">
            <h1>{{ msg }}</h1>
            <div class="mt-4 mb-4">
              <form v-on:submit.prevent="getWeather">
                <label for="ExempleCity" class="mb-3">Quel temps fait il à :</label>
                <div class="d-flex">
                  <input type="text" class="form-control mr-3" placeholder="ville..." v-model="citySearch">
                  <button v-on:click.prevent="getWeather" type="button" class="btn btn-light">ok</button>
                </div>
              </form>
            </div>
            <div>
              <div class="d-flex flex-column mb-2">
                  <span class="font-weight-bold">{{ weather.cityName }}</span>
                <span>{{ weather.description }}</span>
                <span>{{ weather.temperature }}°C</span>
                <div>
                  <span>{{ weather.humidity }}%</span>
                  <span class="pl-1">d'humidité</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    props: {
      msg: String
    },
    data() {
      return {
        citySearch: '',
        weather: {
          cityName: "test",
          country: "NG",
          temperature: 12,
          description: "Clouds everywhere",
          humidity: "55"
        },
      };
    },
    methods: {
      getWeather: async function () {
        console.log(this.citySearch);
        const key = "bd7a6e5ce91cd9060a7c208734b8f387";
        const baseURL =
          `http://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&units=metric&appid=${key}&lang=fr`;
        const response = await fetch(baseURL);
        const data = await response.json();
        console.log(data);
        this.citySearch = "";
        this.weather.cityName = data.name;
        this.weather.country = data.sys.country;
        this.weather.temperature = Math.round(data.main.temp);
        this.weather.description = data.weather[0].description;
        this.weather.humidity = Math.round(data.main.humidity);
      },
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card{
  top: 50%;
  background-color: #f1f1f1;
  border: none;
  label{
    color: #3d3d3d;
  }
  span{
    color: #3d3d3d;
  }
  .form-control{
    border: none;
  }
  .form-control:focus{
      box-shadow: 0 0 0 0.1rem rgba(0,123,255,.25);
  }
  input::placeholder{
    color: #d6d6d6;
  }
}
</style>