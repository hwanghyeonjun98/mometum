<script setup>
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";
import {ref} from "vue";
import axios from "axios";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

const todos = ref([]);
const getTodos = () => {
	axios.get("http://localhost:3000/todos?_sort=id&_order=desc").then((response) => {
		todos.value = response.data;
	});
};
</script>

<template>
	<div class="todo-area">
		<div class="headers">
			<button type="button">
				<font-awesome-icon :icon="['fas', 'window-minimize']" />
			</button>
			<button type="button">
				<font-awesome-icon icon="fa-solid fa-window-maximize" />
			</button>
		</div>
		<div class="todo-body">
			<h4 class="text-capitalize todo-list-title">my todos</h4>
			<TodoForm @getTodos="getTodos" />
			<TodoList :todos="todos" @getTodos="getTodos" />
		</div>
	</div>
</template>

<style>
@import "../../src/assets/css/todo.css";
</style>