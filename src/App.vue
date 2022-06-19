<template>
	<div class="MainWindow">
		<div class="clock">
			<h3 style="margin-top: 10px; margin-left: 10px;">{{ date_str }}</h3>
			<h1 style="margin-top: 10px; margin-left: 10px;">{{ time_str }}</h1>
		</div>
		<h2 class="weatherHeader" style="color: aliceblue">Wetter in {{ location }}</h2>
		<div class="weather">
			<img
				class="weatherIcon"
				v-if="is_sunny"
				src="./assets/sun.png"
			/>
			<img
				class="weatherIcon"
				v-if="is_cloudy"
				src="./assets/cloud.png"
			/>
			<img
				class="weatherIcon"
				v-if="is_rainy"
				src="./assets/rain.png" 
			/>
			<div class="weatherData" style="display: inline-block; margin-left: 10px">
				<h1 style="position: absolute; top: 0; margin-left: 20px;">{{ description }}</h1>
				<h1 style="position: absolute; top: 35px; margin-left: 20px;">{{ temperature }}</h1>
				<h3 style="position: absolute; top: 80px; margin-left: 20px;">Max: {{ temp_max }}</h3>
				<h3 style="position: absolute; top: 100px; margin-left: 20px;">Min: {{ temp_min }}</h3>
			</div>
			
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
		this.getForecast();

		this.startUpdates();
	},
	data() {
		return {
			error_present: false,
			error_message: "",

			datetime: undefined,
			date_str: "",
			time_str: "",

			weather_req_url: "https://api.openweathermap.org/data/2.5/weather?lat=52.279911&lon=8.047179&units=metric&lang=de&appid=375424fb53107d54d2fb666df917ff61",
			weather_forecast_url: "https://api.openweathermap.org/data/2.5/forecast/daily?lat=52.279911&lon=8.047179&cnt=4&units=metric&lang=de&appid=375424fb53107d54d2fb666df917ff61",
			is_sunny: false,
			is_cloudy: false,
			is_rainy: false,
			description: "",
			temperature: "",
			temp_min: "",
			temp_max: "",
			location: ""
		}
	},
	methods: {
		testConnection() {
			// TODO
		},

		/**
		 * gets the current time and updates date string and time string
		 */
		getTime() {	
			this.datetime = new Date();
			this.time_str = this.datetime.toLocaleTimeString();
			this.date_str = this.datetime.toLocaleDateString();
		},

		/**
		 * gets the current weather from openweathermap.org
		 */
		getWeather() {
			axios.get(this.weather_req_url).then((res) => {
				this.description = res.data["weather"][0]["description"];
				let main = res.data["weather"][0]["main"];
				console.log(main);
				if (main === "Clouds") {
					this.is_cloudy = true;
					this.is_sunny = false;
					this.is_rainy = false;
				}
				else if (main === "Sun") {
					this.is_cloudy = false;
					this.is_sunny = true;
					this.is_rainy = false;
				}
				else if (main === "Rain") {
					this.is_cloudy = false;
					this.is_sunny = false;
					this.is_rainy = true;
				}
				this.temperature = res.data["main"]["temp"] + " °C";
				this.temp_max = res.data["main"]["temp_max"] + " °C";
				this.temp_min = res.data["main"]["temp_min"] + " °C";
				this.location = res.data["name"];
				console.log(this.location);
			}).catch((err) => {
				this.error_present = true;
				console.warn(err);
				this.error_message = "Could not retrieve Weather information";
			});
		},

		getForecast() {
			axios.get(this.weather_forecast_url).then((res) => {
				// TODO
				console.log(res);
			}).catch((err) => {
				console.warn(err);
			});
		},

		/**
		 * Sets an interval for time and weather updates
		 */
		startUpdates() {
			setInterval(() => {
				this.getTime();
			}, 1000);

			setInterval(() => {
				this.getWeather();
			}, 1000 * 60);
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
	bottom: 0;
}

.weatherIcon {
	height: 130px;
	margin-left: 10px;
	margin-top: 10px;
	position: absolut;
	left: 0;
}

.weatherHeader {
	position: absolute;
	margin-left: 10px;
	bottom: 135px;
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
