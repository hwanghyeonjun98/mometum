<script setup>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

const emit = defineEmits(["onModalActive", "onFullSize"]);

const modalActive = () => {
	emit("onModalActive");
};

const fullSize = () => {
	emit("onFullSize");
};
</script>

<template>
	<div class="modal-area">
		<div class="modal-wrap">
			<div class="modal-headers">
				<button type="button" @click="modalActive">
					<font-awesome-icon :icon="['fas', 'window-minimize']" />
				</button>
				<button type="button" @click="fullSize">
					<font-awesome-icon icon="fa-solid fa-window-maximize" />
				</button>
			</div>
			<slot name="modal-body"></slot>
		</div>
		<button type="button" class="btn modal-btn" @click="modalActive">
			<slot name="btn-content"></slot>
		</button>
	</div>
</template>


<style scoped>

</style>