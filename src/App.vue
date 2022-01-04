<!--<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Testing first vue app"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>-->
<template>
 <div id="app">
    <Pokemon />
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'App',
  components: {
    Pokemon
  }
}
</script>

<style lang="scss">
 @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');
#app {
  body {
     margin: 0;
    padding: 0;
  }
  
}
</style>



<!--
<script>
import Pokemon from './components/Pokemon.vue'
export default {
  components: {
    Pokemon
  }
}
</script>

<style lang="scss">
  @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');
  body {
    margin: 0;
    padding: 0;
  }
</style>-->
