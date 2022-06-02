<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" v-model="query" class="search-bar" @keypress="fetchWeather" placeholder="Search for a Weather...">
        <!-- <button @click="searchMovie">Search</button> -->
        
      </div>
      <div class="weather-wrap" v-if="typeof weather.main !== 'undefined'" >
        <div class="location-box">
          <div class="location">
            {{weather.name}}, {{weather.sys.country}}
          </div>
          <div class="date">
            {{dateBuilder()}}
          </div>
          <div class="weather-box">
<div class="temp">{{Math.round(weather.main.temp)}}c°</div>
<div class="weather">{{weather.weather[0].main}}</div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      api_key: 'fec01bf025464aafeec17304f08c8653',
      url_base: 'https://api.openweathermap.org/data/2.5/weather',
      query: '',
      weather: {},
    }
  },
  methods: {
    fetchWeather(e) {
      if(e.key == "Enter") {
        fetch(`${this.url_base}?q=${this.query}&units=metric&appid=${this.api_key}`)
       .then(res => {
          return res.json()
        })
        .then(
          this.setResults
        )
      }
    },
    setResults(data) {
      this.weather = data
      console.log(this.weather)
    },
    dateBuilder() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`
    }
  }
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}

body {
  font-family: 'Poppins', sans-serif;
  color:white;
}

#app {
  background-image: url("./assets/bg.jpeg");
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
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  width: 100%;
  display: block;
  padding: 15px;
  border: none;
  border-radius: 0px 15px 0px 15px;
  font-size: 18px;
  font-weight: 500;
  outline: none;
  box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.15);
  background: none;
  background-color: rgba(255, 255, 255, 0.15);
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
  background-color: rgba(255, 255, 255, 0.85);
  border-radius: 15px 0px 15px 0px;
}
.location-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  border-radius: 15px;
  background-color: rgba(0, 0, 0, 0.85);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
}
.location-box .location {
  font-size: 30px;
  font-weight: 500;
  margin-bottom: 10px;
  text-align: center;
  text-shadow: 1px 3px 5px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  font-size: 20px;
  font-weight: 500;
  margin-bottom: 10px;
  text-align: center;
  text-shadow: 1px 3px 5px rgba(0, 0, 0, 0.25);
}
.weather-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  border-radius: 15px;
  background-color: rgba(0, 0, 0, 0.85);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
}
.weather-box .temp {
  
  display: inline-block;
  padding: 10px 25px;
  font-size: 100px;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:  rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
  margin: 30px 0px;
  box-shadow: 3px 8px rgba(244, 240, 240, 0.5);
}

.weather-box .weather {
  font-size: 45px;
  font-weight: 700;
  margin-bottom: 10px;
  font-style: italic;
  text-align: center;
  text-shadow: 1px 3px 5px rgba(0, 0, 0, 0.25);
}

</style>
