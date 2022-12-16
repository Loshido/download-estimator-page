<template>
	<main>
		<header>
			<h1>Download estimator</h1>
			<p>this app gives you the time you will need to download some files, most of the time it used for games.</p>
		</header>
		<section class="inputs">
			<div class="case">
				<input type="number" name="size" id="file-size" min="1" v-model="filesize">
				<select v-model="fileunit">
					<option value="1000000">To (1000 Go)</option>
					<option selected value="1000">Go (1000 Mo)</option>
					<option value="1">Mo (1000 Ko)</option>
					<option value="1/1000">Ko (1000 octets)</option>
				</select>
			</div>
			<div class="case">
				<input type="number" name="speed" id="download-speed" min="1" v-model="speedsize">
				<select v-model="speedunit">
					<option value="1000000">To/s (1 To/s = 8 Tbit/s)</option>
					<option value="1000">Go/s (1 Go/s = 8 Gbit/s)</option>
					<option selected value="1">Mo/s (1 Mo/s = 8 Mbit/s)</option>
					<option value="1/1000">Ko/s (1 Ko/s = 8 Kbit/s)</option>
				</select>
			</div>
		</section>
		<section class="output">
			<div class="case">
				<div class="time" v-text="floor(last / 60 / 60 / 24)"></div>
				<div class="time" v-text="floor(last / 60 / 60)"></div>
				<div class="time" v-text="floor(last / 60)"></div>
				<div class="time" v-text="last"></div>
				<div>Jours</div>
				<div>Heures</div>
				<div>Minutes</div>
				<div>Secondes</div>
			</div>
		</section>
	</main>
</template>

<script setup>
import { evaluate, floor } from "mathjs"
useHead({title: "Download Estimator"});

const filesize = ref(1), fileunit = ref("1000");
const speedsize = ref(1), speedunit = ref("1");

const size = computed(() => filesize.value * evaluate(fileunit.value));
const speed = computed(() => speedsize.value * evaluate(speedunit.value));
const last = computed(() => size.value / speed.value);
</script>