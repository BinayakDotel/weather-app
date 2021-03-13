<template>
  <div id="app">
    <main>
    <input type ="text" 
            id="search-bar"    
           placeholder="Search..."
           v-model="query"
           @keypress="fetchData"/>

    <div id="weather-data" v-if="typeof weather.main!='undefined'">
      <div id="location">
        {{weather.name}}, {{weather.sys.country}}
      </div>
      <div id="temperature">
        {{Math.round(weather.main.temp)}}°C
      </div>
      <div id="condition">
        {{weather.weather[0].main}}
      </div>
    </div>
    </main>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    return{
      weather_api:"96a70247d4844b5786ee94795314e09d",
      basePath:"https://api.openweathermap.org/data/2.5/",
      query:"",
      weather:{}
    }
  },
  methods:{
    fetchData(e){
      if(e.key == "Enter"){
        fetch(`${this.basePath}weather?q=${this.query}&units=metric&APPID=${this.weather_api}`)
        .then(
          response=>{
            return response.json();
          }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather=results;
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
body{
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
#app{
  background-image: url("./assets/background.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main{
  min-height: 100vh;
  padding: 25px;;
}
#search-bar{
  display: block;
  width: 100%;
  padding: 20px;

  appearance: none;
  border: none;
  background: none;

  background-color: rgba(219, 211, 207, 0.76);
  float:center;
  border-radius: 10px;
}
#weather-data {
  color: white;
  background-color:rgba(199, 154, 241, 0.089);
  border-radius: 20px;
}
#location{
  padding-top: 20px;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 1px rgb(255, 154, 60);
}
#temperature{
  padding-top: 20px;
  font-size: 20px;
  font-weight: 200;
  font-style: italic;
  text-align: center;
  text-shadow: 1px 1px rgba(235, 163, 97, 0.863);
}
#condition{
  padding-top: 15px;
  font-size: 25px;
  font-weight: 300;
  text-align: center;
  text-shadow: 1px 1px rgb(255, 154, 60);
}
</style>
