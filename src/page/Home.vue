<script setup>
import Time from "@/components/time/Time.vue";
import Todo from "@/components/todo/Todo.vue";
import Intoro from "@/components/intro/Intro.vue";
import Setting from "@/components/setting/Setting.vue";

</script>

<template>
	<div class="background">
		<Time />
		<Intoro />
		<div class="tmp">

		</div>
		<Todo />
		<Setting />
	</div>
</template>

<style scoped>
@import "../../src/assets/css/home.css";

/*.tmp {
	width: 100%;
	min-height: 30vh;
}*/
</style>