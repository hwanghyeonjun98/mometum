<script setup>
import {ref} from "vue";
import axios from "axios";

const emit = defineEmits(["getTodos"]);

const todoInput = ref("");

const todoAdd = () => {
	const todoItem = {
		content   : todoInput.value,
		isChecked : false,
		created   : new Date().getTime(),
	};

	axios.post("http://localhost:3000/todos", todoItem, {
		headers : {
			"Content-Type" : "application/json",
		},
	}).then(() => {
		emit("getTodos");
		todoInput.value = "";
	});
};
</script>

<template>
	<form id="todo-form" @submit.prevent>
		<input type="text" id="todo" v-model="todoInput" name="todo" placeholder="오늘 할일을 입력하세요." />
		<button type="submit" @click="todoAdd">추가</button>
	</form>
</template>

<style scoped>

</style>