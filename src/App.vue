<!--
  un module vue se compose en général de :
  une template contenant le HTML du module,
  une partie script contenant le javascript et l'export du module
  une partie style pour des changements de style locaux.
-->

<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to your Vue.js App"/>
  <li>ce li n'est pas rouge!</li>
</template>

<script>
//voir le main.js pour comprendre l'affichage de App
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<!--
  ce style n'ayant pas l'attribut scoped, il s'appliquera partout, même dans ses composants parents.
-->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
