<script setup>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import FloatModal from "@/components/floatmodal/FloatModal.vue";
import TodoList from "@/components/TodoList.vue";
import TodoForm from "@/components/TodoForm.vue";
import {ref} from "vue";

const isModalctive = ref(false);
const isFullScreen = ref(false);

const modalActive = () => {
	isModalctive.value = !isModalctive.value;
	console.log("isModalctive.value,", isModalctive.value);

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
		class="bottom-left"
		@onFullSize="fullSize"
		@onModalActive="modalActive"
	>
		<template #modal-body>
			<div class="modal-body setting-body">
				<ul>
					<li>

					</li>
				</ul>
			</div>
		</template>
		<template #btn-content>
			<font-awesome-icon :icon="['fas', 'gear']" />
			<span class="text-capitalize">setting</span>
		</template>
	</FloatModal>
</template>

<style scoped>

</style>