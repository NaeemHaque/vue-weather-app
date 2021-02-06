<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input 
        type="search" 
        class="search-bar" 
        placeholder="Search Your Loaction..."
        v-model="query"
        @keypress="fetchWeather"
        >
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'" >
        
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>


<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: '1a61d5466a3cd91839f425c7837c7a25',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}

    }
   
  },
   methods: {
      fetchWeather(e){
        if(e.key == "Enter"){
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json()
          }).then(this.setResult)
          
        }
      },
      setResult(results){
        this.weather = results
      },
      dateBuilder(){
        let d = new Date();
        let months = [
          "January", "February", "March", 
          "April", "May", "june", "July", 
          "August", "September", "October", 
          "November", "December"
        ];
        let days = [
          "Sunday",
          "Monday",
          "Tuesday",
          "Wednessday",
          "Thursday",
          "Friday",
          "Saturday"]

          let day = days[d.getDay()];
          let date = d.getDate();
          let month = months[d.getMonth()];
          let year = d.getFullYear();

          return `${day} || ${date}-${month}-${year}`;
      }
    }
}

</script>


<style>

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
font-family: 'montserrat', sans-serif ;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}
.search-box {
  width: 80%;
  margin: 0 auto;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  background-color: rgba(255, 255, 255, 0.5);
  box-shadow:0px 0px 8px rgba(0, 0, 0, 0.25);
  border-radius: 0px 15px 0px 15px;
  transition: 0.4s;
}
.search-box .search-bar:focus{
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow:0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);
  margin-top: 30px;
}

.location-box .date {
  color: white;
  font-size: 20px;
  font-weight: 100;
  text-align: center;
  font-style: italic;
  margin-top: 5px;
}
.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 15px, 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  
  box-shadow: 4px 7px rgba(0, 0, 0, 0.25);
}
  
.weather-box .weather {
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>