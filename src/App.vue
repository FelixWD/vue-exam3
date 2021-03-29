<template>
  <div id="app1" :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Clear' ? 
  'clear' : '' ">
  <div id="app2" :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Drizzle' ?
  'clouds' : ''">
  <div id="app3" :class="typeof weather.main != 'undefined' && weather.weather[0].main =='Rain' ?
  'rain' : ''">
    <div id="app4" :class="typeof weather.main != 'undefined' && weather.weather[0].main =='Snow' ?
  'snow' : ''">
    <div id="app5" :class="typeof weather.main != 'undefined' && weather.weather[0].main =='Thunderstorm' ?
  'thunder' : ''">
    <main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Enter City (&) Country"
        v-model="query"
        @keypress="fetchWeather"
        />
      </div>

      <div class="main-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="main-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateProg() }}</div>
          <div class="time">{{ curTime() }}</div>
          <div class="condition">{{ weather.weather[0].main }}</div>
     <div class="second-box">
       <div class="temperature">{{ Math.round(weather.main.temp) }}°c</div>
       </div>
       </div>
       </div>
 <div class="row justify-content-center">
    <div class="justify-content-center text-center">
      <div class="input-group-append">
        <button @click="updateLocation" class="btn btn-outline-secondary"
        type="button">5 Day Forecast</button>
      </div>
      </div>
       </div>
    </main>
  </div>
  </div>
  </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      API_KEY: '4b1320c4e78a9f93966826bd7a294627',
      API_URL: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.keyCode == 13) {
        fetch(`${this.API_URL}weather?q=${this.query}&units=metric&APPID=${this.API_KEY}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },

    setResults (results) {
      this.weather = results;
    },
    dateProg () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", 
      "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday",
      "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },
    curTime (){
      var tdiff = this.weather.timezone;
      var vMili = tdiff * 1000;
      var x = new Date().getTime();
      var z = x + vMili;
      var y = new Date(z).toISOString().slice(11, -8);
      return y;

    }
  },
}

</script>


<style>

* {
  margin: 0;
  padding: 0;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
}

@font-face { font-family: "Sunflower";
  src: local("Sunflower"),
  url(./assets/Sunflower.otf) 
  format("opentype");
}

body {
  font-family: "Sunflower", Helvetica, Arial;
}


#app {
  background-image: url('./assets/sunnycloud.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}

#app1.clear {
  background-image: url('./assets/clear.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}

#app2.clouds {
  background-image: url('./assets/clouds.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;  
}

#app3.rain {
  background-image: url('./assets/rain.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}

#app4.snow {
  background-image: url('./assets/snow.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}

#app5.thunder {
  background-image: url('./assets/thunder.jpg');
  background-size: cover;
  background-position: bottom;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
}


main {
  min-height: 100vh;
  padding: 30px;
  background-image: -webkit-gradient(linear, left top, left bottom, from(rgba(0, 0, 0, 0.15)), to(rgba(0, 0, 0, 0.85)));
  background-image: -o-linear-gradient(top, rgba(0, 0, 0, 0.15), rgba(0, 0, 0, 0.85));
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.15), rgba(0, 0, 0, 0.85));
}

.search-box {
  width: 400px;
  margin: 0 auto;
  text-decoration: none;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 12px;
  color: #636363f5;
  font-size: 20px;
  font-style: italic;

  -webkit-appearance: none;

     -moz-appearance: none;

          appearance: none;
  border: none;
  outline: none;
  background: none;

  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 4px 4px 0px 0px;
  -webkit-transition: 0.5s;
  -o-transition: 0.5s;
  transition: 0.5s;
  text-decoration: none;
}

.search-box .search-bar:focus {
  -webkit-box-shadow: 0px 0px 12px rgba(0, 0, 0, 0.30);
          box-shadow: 0px 0px 12px rgba(0, 0, 0, 0.30);
  background-color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
}

.main-wrap {
  background-color: rgb(140, 140, 140, 0.3);
  width: 400px;
  margin: 0 auto;
  border-radius: 0px 0px 12px 12px;
}

.main-box .location {
  color: #FFFFFF;
  font-size: 34px;
  font-weight: 600;
  text-align: center;
  text-shadow: 2px 4px rgba(0, 0, 0, 0.3);
}

.main-box .date {
  color: #FFFFFF;
  font-size: 22px;
  font-weight: 400;
  text-align: center;
  font-style: italic;
  text-shadow: 2px 2px rgba(0, 0, 0, 0.2);
}

.main-box .time {
  color: #FFFFFF;
  font-size: 24px;
  font-weight: 500;
  text-align: center;
  text-shadow: 2px 2px rgba(0, 0, 0, 0.2);
}

.condition {
  color: #FFFFFF;
  font-size: 36px;
  font-weight: 400;
  text-align: center;
  font-style: italic;
  text-shadow: 2px 2px rgba(0, 0, 0, 0.3);
  margin: 30px 0px;
}


.second-box {
  text-align: center;
}

.second-box .temperature {
  display: inline-block;
  margin: 10px 0px;
  padding: 10px;
  color: #FFFFFF;
  font-size: 80px;
  font-weight: 700;
  text-shadow: 2px 4px rgba(0, 0, 0, 0.3);
}

.btn {
  margin-top: 20px;
  font-size: 18px;
  color: #f3f3f3;
  border-color: rgba(172, 172, 172, 0.8);
}


@media screen and (max-width: 600px) {
  .main-wrap {
    width: 200px;
  }
}

@media screen and (max-width: 600px) {
  .search-box {
    width: 200px;
  }
}
</style>