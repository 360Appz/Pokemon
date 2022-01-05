
<!--Template provides a HTML-based syntax
to bind the rendered DOM to an underlying
Vue instance data -->
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

<!-- SCSS is more advance than regular CSS, 
requires less code, allows nested code which improves 
readability when scaling a project-->
<style lang="scss">
 @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');
#app {
  body {
     margin: 0;
    padding: 0;
  }
  
}
</style>




