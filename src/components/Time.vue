<script setup>
import {onMounted, ref} from "vue";

const hour = ref();
const minute = ref();
const second = ref();
const ampm = ref("");

const time = () => {
	let date = new Date();
	hour.value = String(date.getHours()).padStart(2, "0");
	minute.value = String(date.getMinutes()).padStart(2, "0");
	second.value = String(date.getSeconds()).padStart(2, "0");
	ampm.value = hour % 12 > 0 ? "am" : "pm";
};

onMounted(() => {
	time();

	setInterval(() => {
		time();
	}, 1000);
});

</script>

<template>
	<div class="time-area">
		<ul class="time">
			<li>{{ hour }}</li>
			<li>:</li>
			<li>{{ minute }}</li>
			<li>:</li>
			<li>{{ second }}</li>
			<li class="text-uppercase ampm">{{ ampm }}</li>
		</ul>
	</div>
</template>

<style scoped>
@import "../../src/assets/css/time.css";
</style>