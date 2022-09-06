<template>
  <main>
    <div class="searchBox">
      <input type="text" v-model="getQuery" class="searchBar" placeholder="Search..." @keypress="getWeatherDetail" />
    </div>
    <div class="weaterWrap" v-if="typeof weather.main != 'undefined'">
    
      <div class="locationbox">
        <div class="location">{{weather.name}} {{weather.sys.country}}°c</div>
        <div class="date">{{getDayDate()}}</div>
      </div>
      <div class="weatherBox">
        <div class="temp">{{Math.round(weather.main.temp)}}</div>
        <div class="weather"> {{weather.weather[0].main}} </div>
      </div>
    </div>
  </main>
</template>
<!-- 
      { "coord": { "lon": 88.3697, "lat": 22.5697 }, "weather": [ { "id": 721, "main": "Haze", "description": "haze", "icon": "50n" } ], "base": "stations", "main": { "temp": 27.97, "feels_like": 32.49, "temp_min": 27.97, "temp_max": 27.97, "pressure": 1007, "humidity": 83 }, "visibility": 2800, "wind": { "speed": 0, "deg": 0 }, "clouds": { "all": 75 }, "dt": 1662483423, "sys": { "type": 1, "id": 9114, "country": "IN", "sunrise": 1662421840, "sunset": 1662466788 }, "timezone": 19800, "id": 1275004, "name": "Kolkata", "cod": 200 }
     -->
<script>
export default {
  name: "app",
  data() {
    return {
      apiKey: "0da4bb0ec74364eed42320414bb3729c",
      baseUrl: "https://api.openweathermap.org/data/2.5/",
      getQuery: "",
      weather: {},
    };
  },
  methods: {
    getWeatherDetail(e) {
      if (e.key == "Enter") {
        fetch(`${this.baseUrl}weather?q=${this.getQuery}&units=metric&APPID=${this.apiKey}`)
        .then(res =>{
          return res.json()
        }).then(this.setWeatherDetail)
      }
    },
    setWeatherDetail(results){
      this.weather = results
      console.log(this.weather)
    },
    getDayDate(){
      let dt = new Date();
      let mnth = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let dys = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      
      let day = dys[dt.getDay()];
      let date = dt.getDate();
      let month = mnth[dt.getMonth()];
      let year = dt.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  },
};
</script>
<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}
.searchBox {
  width: 100%;
  margin-bottom: 30px;
  .searchBar {
    display: block;
    width: 100%;
    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    border: none;
    outline: none;
    box-shadow: 0px 0px 8px rgba($color: #000000, $alpha: 0.25);
    background-color: rgba($color: #ffffff, $alpha: 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
    &:focus {
      box-shadow: 0px 0px 16px rgba($color: #000000, $alpha: 0.25);
      border-radius: 16px 0px 16px 0px;
      background-color: rgba($color: #ffffff, $alpha: 0.75);
    }
  }
}
.weaterWrap {
  text-align: center;
  color: #ffffff;
  .locationbox {
    margin-bottom: 15px;
    .location {
      margin-bottom: 15px;
      font-size: 35px;
      font-weight: 600;
      text-shadow: 1px 3px rgba($color: #000000, $alpha: 0.25);
    }
    .date {
      font-size: 20px;
      font-weight: 300;
      font-style: italic;
    }
  }
}
.weatherBox {
  .temp {
    display: inline-block;
    padding: 20px;
    font-size: 105px;
    font-weight: 900;

    text-shadow: 3px 6px rgba($color: #000000, $alpha: 0.25);
    background-color: rgba($color: #ffffff, $alpha: 0.5);
    border-radius: 16px;
    margin: 30px;
    box-shadow: 3px 6px rgba($color: #000000, $alpha: 0.25);
  }
  .weather {
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba($color: #000000, $alpha: 0.25);
  }
}
</style>
