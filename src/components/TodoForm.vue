<script setup>
import {ref} from "vue";
import axios from "axios";

const emit = defineEmits(["getTodos"]);

const todoInput = ref("");

const onTodoAdd = () => {
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
const todoAdd = () => {
	if (todoInput.value === "") {
		alert("할일을 입력하세요!");
		return false;
	}
	onTodoAdd();
};
</script>

<template>
	<form id="todo-form" @submit.prevent>
		<input type="text" id="todo" v-model="todoInput" name="todo" placeholder="오늘 할일을 입력하세요." />
		<button type="submit" class="btn-round submit-btn" @click="todoAdd">추가</button>
	</form>
</template>

<style scoped>
form {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 1rem;
	background-color: #fafafa;
}

form input {
	flex: 3 1 auto;
}

form button {
	flex: 0 0 4rem;
}

.submit-btn {
	transition: all .2s ease-in-out;
}

.submit-btn:hover {
	background-color: #aeaeae;
}
</style>