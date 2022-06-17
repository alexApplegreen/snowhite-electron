<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>

  <button
	class="pure-button pure-button-primary"
	@click="partymode()"
  >
	Partymode!
  </button>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import swal from 'sweetalert2'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
	partymode() {
		swal.fire("Partymode, Bitches!");
	}
  }
}
</script>

<style>
@import "~purecss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
