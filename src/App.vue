<template>
  <div id="app">
    <div class="container">
      <div class="search-box">
        <input type="text" placeholder="search....!!!" class="search-bar">
      </div>

      <div class="weather-wrap" v-if="weather.main">
        <div class="location-box">
          <div class="location">{{weather.name}}</div>
          <div class="date">Octorber 8th 2020</div>
        </div>
        <div class="weather-box">
          <div class="temperature">{{Math.round(weather.main.temp)}}°C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'App', 
  data(){
    return{
      api_key: process.env.VUE_APP_WEATHER_KEY,
      base_url: 'https://api.openweathermap.org/data/2.5/',
      query: 'china',
      weather: {},
      date: ''
    }
  }, 
  methods: {
      async fetchWeather() {
        const data = await fetch('${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}')
        this.weather = await data.json()
      }
  },
  created() { 
    this.fetchWeather();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: 50%;
  transition: 0.5s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

.container {
  height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  )
}

/* 搜尋框的部分，占滿整個寬度、邊角稍微好看一些，由於在輸入時我們希望做一點簡單的變化，所以加入transition屬性 */
.search-box {
  width: 100%;
  margin-bottom: 35px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  transition: all 0.4s ease-in;
  border-radius: 0 16px 0 16px;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;
  background-color: hsla(0,0%,100%,.5);
}

/* 加入focus時邊框的變化，看起來就會更有質感一點點 */
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius: 16px 0px 16px 0px;
}

/* 需要的只是置中並在字體跟背景動點手腳 */
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}

/* weather-box的部分也是同樣也需要置中 */
.weather-box {
  text-align: center;
  margin-top: 15px;
}

/* 顯示溫度的部分需要大塊的背景空白與粗字體 */
.weather-box .temperature {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

/* 天氣的部分則需要稍小的粗體字 */
.weather-box .weather {
  font-size: 48px;
  color: #fff;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

</style>
