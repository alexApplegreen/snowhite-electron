<template>
	<div class="MainWindow">
		<div class="clock">
			<h3 style="margin-top: 10px; margin-left: 10px;">{{ date_str }}</h3>
			<h1 style="margin-top: 10px; margin-left: 10px;">{{ time_str }}</h1>
		</div>
		<div class="weather">
			<h1 class="widgetHeader">Weather</h1>
		</div>
		<div class="mails">
			<h1 class="widgetHeader">Mails</h1>
		</div>
		<div class="calendar">
			<h1 class="widgetHeader">Calendar</h1>
		</div>
	</div> 
</template>

<script>

export default {
	name: 'App',
	mounted() {
		this.getTime();
	},
	data() {
		return {
			datetime: undefined,
			date_str: "",
			time_str: "",	
		}
	},
	methods: {
		getTime() {	
			setInterval(() => {
				this.datetime = new Date();
				this.time_str = this.datetime.toLocaleTimeString();
				this.date_str = this.datetime.toLocaleDateString();
			}, 1000)
		}	
	}
}
</script>

<style>
@import "~purecss";

.MainWindow {
	color: aliceblue;
	overflow-y: hidden;
	overflow-x: hidden;
	height: 1080px;
	width: 1920px;
	background-color: black;
}

.widgetHeader {
	color:aliceblue;
	margin-top: 10px;
	margin-left: 10px;
}

.clock {
	position: absolute;
	height: 150px;
	width: 300px;
	top: 0;
	left: 0;
}

.weather {
	position: absolute;
	height: 150px;
	width: 99%;
	border: 1px solid white;
	border-radius: 4px;
	bottom: 0;
}

.mails {
	position: absolute;
	height: 150px;
	width: 300px;
	border: 1px solid white;
	border-radius: 4px;
	right: 0;
	top: 0;
}

.calendar {
	position: absolute;
	height: 500px;
	width: 300px;
	border: 1px solid white;
	border-radius: 4px;
	right: 0;
	top: 300px;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
</style>
