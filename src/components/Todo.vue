<script setup>
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";
import {ref} from "vue";
import axios from "axios";

const todos = ref([]);
const getTodos = () => {
	axios.get("http://localhost:3000/todos?_sort=id&_order=desc").then((response) => {
		todos.value = response.data;
	});
};
</script>

<template>
	<div class="todo-area">
		<TodoForm @getTodos="getTodos" />
		<h4 class="text-capitalize">my todo list</h4>
		<TodoList :todos="todos" @getTodos="getTodos" />
	</div>
</template>

<style scoped>

</style>