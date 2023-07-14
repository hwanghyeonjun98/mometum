<script setup>
import TodoItem from "@/components/todo/TodoItem.vue";

const {todos} = defineProps({
	todos : {
		type     : Array,
		required : true,
	},
});

const emit = defineEmits(["getTodos"]);

const getTodos = () => {
	emit("getTodos");
};

</script>

<template>
	<ul class="todo-list">
		<TodoItem
			v-for="todo in todos"
			:key="todo.created"
			:todo="todo"
			:todos="todos"
		/>
	</ul>
</template>

<style>

</style>