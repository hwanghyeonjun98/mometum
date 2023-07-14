<script setup>
import {ref} from "vue";

const emit = defineEmits(["getTodos", "onTodoAdd"]);

const todoInput = ref("");

const todoAdd = () => {
	if (todoInput.value === "") {
		alert("할일을 입력하세요!");
		return false;
	}

	const todoItem = {
		content   : todoInput.value,
		isChecked : false,
		created   : new Date().getTime(),
	};

	emit("onTodoAdd", todoItem);

	todoInput.value = "";
};
</script>

<template>
	<form id="todo-form" @submit.prevent>
		<input type="text" id="todo" v-model="todoInput" name="todo" placeholder="오늘 할일을 입력하세요." />
		<button type="submit" class="btn btn-round submit-btn" @click="todoAdd">추가</button>
	</form>
</template>

<style>

</style>