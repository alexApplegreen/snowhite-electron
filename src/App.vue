<template>
	<div class="MainWindow">
		<h1>Hallo Welt</h1>
		<button
			class="pure-button pure-button-primary"
			@click="partymode()"
		>
			Partymode!
		</button>
	</div> 
</template>

<script>
import swal from 'sweetalert2'

export default {
  name: 'App',
  methods: {
    partymode() {
      swal.fire("Partymode, Bitches!");
    }
  }
}
</script>

<style>
@import "~purecss";

.MainWindow {
	background-color: black;
	text-align: center;
	color: aliceblue;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
}
</style>
