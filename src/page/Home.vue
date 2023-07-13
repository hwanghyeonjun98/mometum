<script setup>
import Time from "@/components/Time.vue";
import Todo from "@/components/Todo.vue";
import Intoro from "@/components/Intro.vue";
import Setting from "@/components/Setting.vue";
</script>

<template>
	<div class="background">
		<Time />
		<Intoro />
		<Todo />
		<Setting />
	</div>
</template>

<style scoped>
@import "../../src/assets/css/home.css";
</style>