<script setup>
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";
</script>

<template>
	<div class="todo-area">
		<TodoForm />
		<h4 class="text-capitalize">my todo list</h4>
		<TodoList />
	</div>
</template>

<style scoped>

</style>