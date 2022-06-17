<template>
	<div class="MainWindow">
		<h1>Hallo Welt</h1>
	</div> 
</template>

<script>

export default {
	name: 'App',
	data() {
		return {
			
		}
	},
	methods: {
		
	}
}
</script>

<style>
@import "~purecss";

.MainWindow {
	text-align: center;
	color: aliceblue;
	overflow-y: hidden;
	overflow-x: hidden;
	height: 1080px;
	width: 1920px;
	background-color: black !important;
}

.forecast_embed {
	position: absolute;
	bottom: 0;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
</style>
