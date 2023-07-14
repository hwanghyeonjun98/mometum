<script setup>
import {ref} from "vue";

const {todo, todos} = defineProps({
	todo  : {
		type     : Object,
		required : true,
	},
	todos : {
		type     : Array,
		required : true,
	},
});

const checked = ref(todo.isChecked);

const todoDelete = () => {
	const index = todos.indexOf(todo);
	todos.splice(index, 1);

	localStorage.setItem("todos", JSON.stringify(todos));
};

const todoUpdate = () => {
	const index = todos.indexOf(todo);
	todos[index] = {
		...todos[index],
		isChecked : !checked.value,
	};

	localStorage.setItem("todos", JSON.stringify(todos));
};
</script>

<template>
	<li class="todo">
		<div :class="checked ? 'completed' : ''" class="todo-color-bar"></div>
		<div :class="checked ? 'completed' : ''" class="todo-content">
			<div class="todo-checkbox">
				<input
					type="checkbox"
					:id="`todo-check-${todo.created}`"
					v-model="checked"
					name="todo"
					@click="todoUpdate"
				>
				<span></span>
			</div>
			<p :class="checked ? 'completed' : ''" class="todo-text">
				<label :for="`todo-check-${todo.created}`">{{ todo.content }}</label>
			</p>
		</div>
		<div class="delete">
			<button type="button" class="btn btn-round delete-btn" @click="todoDelete">
				<font-awesome-icon :icon="['fas', 'trash-can']" />
			</button>
		</div>
	</li>
</template>

<style>
</style>