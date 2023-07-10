<script setup>
import { onMounted, ref } from "vue";

const hour = ref();
const minute = ref();
const second = ref();
const ampm = ref("");

onMounted(() => {
	setInterval(() => {
		const date = new Date();
		hour.value = date.getHours();
		minute.value = date.getMinutes();
		second.value = date.getSeconds();

		ampm.value = "pm";
	}, 1000);
});

</script>

<template>
	<div>
		<ul>
			<li>{{ hour }}</li>
			<li>{{ minute }}</li>
			<li>{{ second }}</li>
			<li>{{ ampm }}</li>
		</ul>
	</div>
</template>

<style scoped>

</style>