<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/poke.svg.png" width="400px">
    <HelloWorld msg="Poke Api con Vue"/>
    <rick-morty></rick-morty>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import RickMorty from './components/rickmorty.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    "rick-morty": RickMorty
  }
}
</script>

<style>
#app{
  text-align: center;
}
</style>
