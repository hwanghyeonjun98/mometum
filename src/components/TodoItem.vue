<script setup>
import axios from "axios";
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
		`http://localhost:3000/todos/${id}`,
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
		<div class="todo-content">
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
			<button type="button" @click="todoDelete(todo.id)">삭제</button>
		</div>
	</li>
</template>

<style scoped>
.todo,
.todo-content {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.todo {
	padding: .5rem;
	margin-bottom: 1rem;
	border-bottom: 1px solid rgba(0, 0, 0, .2);
}

.todo-text {
	margin: 0;
}

.todo-text label {
	padding: .5rem;
}

</style>