<script setup>
import axios from "@/config/axios";
import {ref} from "vue";

const {todo} = defineProps({
	todo : {
		type     : Object,
		required : true,
	},
});

const emit = defineEmits(["onTodoDelete"]);

const checked = ref(todo.isChecked);

const todoDelete = (id) => {
	emit("onTodoDelete", id);
};

const inputCheck = (id) => {
	axios.patch(
		`/todos/${id}`,
		{...todo, isChecked : !checked.value},
		{
			headers : {
				"Content-Type" : "application/json",
			},
		},
	);
};
</script>

<template>
	<li class="todo">
		<div :class="checked ? 'completed' : ''" class="todo-color-bar"></div>
		<div :class="checked ? 'completed' : ''" class="todo-content">
			<div class="todo-checkbox">
				<input
					type="checkbox"
					:id="`todo-check-${todo.id}`"
					v-model="checked"
					name="todo"
					@click="inputCheck(todo.id)"
				>
				<span></span>
			</div>
			<p :class="checked ? 'completed' : ''" class="todo-text">
				<label :for="`todo-check-${todo.id}`">{{ todo.content }}</label>
			</p>
		</div>
		<div class="delete">
			<button type="button" class="btn btn-round delete-btn" @click="todoDelete(todo.id)">
				<font-awesome-icon :icon="['fas', 'trash-can']" />
			</button>
		</div>
	</li>
</template>

<style>
</style>