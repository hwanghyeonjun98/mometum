<script setup>
import TodoItem from "@/components/TodoItem.vue";
import {onMounted} from "vue";
import axios from "@/config/axios";

const {todos} = defineProps(["todos"]);

const emit = defineEmits(["getTodos"]);

const getTodos = () => {
	emit("getTodos");
};

onMounted(() => {
	getTodos();
});

const todoDelete = (id) => {
	axios.delete(`/todos/${id}`).then(() => {
		getTodos();
	});
};

</script>

<template>
	<ul class="todo-list">
		<TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @onTodoDelete="todoDelete" />
	</ul>
</template>

<style>

</style>