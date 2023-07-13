<script setup>
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";
import {ref} from "vue";
import axios from "@/config/axios";
import FloatModal from "@/components/floatmodal/FloatModal.vue";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

const isModalctive = ref(false);
const isFullScreen = ref(false);

const todos = ref([]);
const getTodos = () => {
	axios.get("/todos?_sort=id&_order=desc").then((response) => {
		todos.value = response.data;
	});
};

const modalActive = () => {
	isModalctive.value = !isModalctive.value;
	console.log("emit", isModalctive.value);

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
				<TodoForm @getTodos="getTodos" />
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
@import "../../src/assets/css/todo.css";
</style>