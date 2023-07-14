<script setup>
import TodoForm from "@/components/todo/TodoForm.vue";
import TodoList from "@/components/todo/TodoList.vue";
import {onMounted, ref} from "vue";
import FloatModal from "@/components/floatmodal/FloatModal.vue";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

const localTodos = localStorage.getItem("todos");
const todoJson = JSON.parse(localTodos);

const isModalctive = ref(false);
const isFullScreen = ref(false);

const todos = ref([]);

const getTodos = () => {
	todoJson.sort((a, b) => b.created - a.created);

	todos.value = todoJson;
};

onMounted(() => {
	if (todoJson !== null) {
		getTodos();
	}
});

const todoAdd = (item) => {
	todos.value.unshift(item);

	localStorage.setItem("todos", JSON.stringify(todos.value));
};

const modalActive = () => {
	isModalctive.value = !isModalctive.value;

	if (isModalctive.value === false) {
		isFullScreen.value = false;
	}
};

const fullSize = () => {
	isFullScreen.value = !isFullScreen.value;
};

</script>

<template>
	<FloatModal
		:class="[`${isModalctive ? 'active' : ''}`, `${isFullScreen ? 'full-size': ''}`]"
		class="todo-area bottom-right"
		@onFullSize="fullSize"
		@onModalActive="modalActive"
	>
		<template #modal-body>
			<div class="modal-body todo-body">
				<h4 class="text-capitalize todo-list-title">my todos</h4>
				<TodoForm @getTodos="getTodos" @onTodoAdd="todoAdd" />
				<TodoList :todos="todos" @getTodos="getTodos" />
			</div>
		</template>
		<template #btn-content>
			<font-awesome-icon :icon="['fas', 'file-pen']" />
			<span class="text-uppercase">todo</span>
		</template>
	</FloatModal>
</template>

<style>
@import "../../assets/css/todo.css";
</style>