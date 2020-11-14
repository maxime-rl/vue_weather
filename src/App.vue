<template>
  <div id="app">
    <Home msg="App Météo"/>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
#app{
  height: 100vh;
  font-family: 'Lato', sans-serif;
  background-color: #fdfdfd;
}
h1,h2,h3,h4,h5,h6{
      color: #3d3d3d;
}
h1{
  font-size: 2rem;
  font-weight: 700;
}

li{
  list-style: none;
};

</style>
