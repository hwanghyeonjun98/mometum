<script setup>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import FloatModal from "@/components/floatmodal/FloatModal.vue";
import {ref} from "vue";

const isTime12 = ref(false);
const isModalctive = ref(true);
const isFullScreen = ref(false);

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
		class="setting-area bottom-left"
		@onFullSize="fullSize"
		@onModalActive="modalActive"
	>
		<template #modal-body>
			<div class="modal-body setting-body">
				<ul class="setting-list">
					<li class="setting-item">
						<span class="setting-title">이름 변경</span>
						<button type="button" class="setting-btn">
							<font-awesome-icon :icon="['fas', 'caret-right']" />
						</button>
					</li>
					<li class="setting-item">
						<span class="setting-title"><label for="isTime12">2시간제</label></span>
						<label for="isTime12">
							<span class="toggle-btn-sm">
								<input type="checkbox" id="isTime12" v-model="isTime12" class="toggle-checkbox" name="isTime12">
								<span class="toggle-backgound"></span>
								<span class="toggle"></span>
							</span>
						</label>
					</li>
				</ul>
			</div>
		</template>
		<template #btn-content>
			<font-awesome-icon :icon="['fas', 'gear']" />
			<span class="text-capitalize">setting</span>
		</template>
		<template #etc>
			<div class="setting-modal">
				<div class="name-edit-modal">
					<h4>이름 수정</h4>
					<label class="hidden" for="nameEdit">이름 수정</label>
					<input type="text" id="nameEdit" name="nameEdit">
					<button type="button">수정</button>
				</div>
			</div>
		</template>
	</FloatModal>


</template>

<style>
@import "../../assets/css/setting.css";
</style>