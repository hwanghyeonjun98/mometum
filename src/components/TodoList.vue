<script setup>
import TodoItem from "@/components/TodoItem.vue";
import {onMounted, ref} from "vue";
import axios from "axios";

const todos = ref([]);

const getTodos = () => {
	axios.get("http://localhost:3000/todos").then((response) => {
		todos.value = response.data;
	});
};

onMounted(() => {
	getTodos();
});

const todoDelete = (id) => {
	axios.delete(`http://localhost:3000/todos/${id}`).then(() => {
		getTodos();
	});
};

</script>

<template>
	<ul class="todo-list">
		<TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @onTodoDelete="todoDelete" />
	</ul>
</template>

<style scoped>

</style>