<template>
	<div class="MainWindow">
		<div class="clock">
			<h3 style="margin-top: 10px; margin-left: 10px;">{{ date_str }}</h3>
			<h1 style="margin-top: 10px; margin-left: 10px;">{{ time_str }}</h1>
		</div>
		<div class="weather">
			<img
				class="weatherIcon"
				v-if="is_sunny" 
				src="./assets/sun.png"
			/>
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
import axios from 'axios';

export default {
	name: 'App',
	mounted() {
		this.testConnection();
		this.getTime();
		this.getWeather();
	},
	data() {
		return {
			error_present: false,
			error_message: "",

			datetime: undefined,
			date_str: "",
			time_str: "",

			weather_req_url: "https://api.openweathermap.org/data/2.5/weather?lat=52.279911&lon=8.047179&units=metric&appid=375424fb53107d54d2fb666df917ff61&lang=de",
			is_sunny: true,
			is_cloudy: false
		}
	},
	methods: {
		testConnection() {
			// TODO
		},

		getTime() {	
			setInterval(() => {
				this.datetime = new Date();
				this.time_str = this.datetime.toLocaleTimeString();
				this.date_str = this.datetime.toLocaleDateString();
			}, 1000)
		},

		getWeather() {
			setInterval(() => {
					axios.get(this.weather_req_url).then((res) => {
					console.log(res);
					// TODO parse and display
				}).catch(() => {
					this.error_present = true;
					this.error_message = "Could not retrieve Weather information";
				});
			}, 1000 * 60)
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

.weatherIcon {
	height: 130px;
	margin-left: 10px;
	margin-top:10px
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
