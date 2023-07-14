<script setup>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import FloatModal from "@/components/floatmodal/FloatModal.vue";
import {ref, watch} from "vue";

const storage = localStorage.getItem("time12");
const isTime12 = ref(storage);
const isModalctive = ref(false);
const isFullScreen = ref(false);
const isNameEditModal = ref(false);

const editName = ref("");

const {isSuccess, formInfoMessage} = defineProps({
	isSuccess       : {
		type     : Boolean,
		required : false,
	},
	formInfoMessage : {
		type     : String,
		required : false,
	},
	isInfoVisible   : {
		type     : Boolean,
		required : false,
	},
});

const emit = defineEmits(["onNameEdit"]);

const modalActive = () => {
	isModalctive.value = !isModalctive.value;

	if (isModalctive.value === false) {
		isFullScreen.value = false;
	}
};

const fullSize = () => {
	isFullScreen.value = !isFullScreen.value;
};

const nameEdit = () => {
	emit("onNameEdit", editName.value);

	editName.value = "";
};

const nameEditEnter = (event) => {
	if (event.keyCode === 13) {
		emit("onNameEdit", editName.value);

		editName.value = "";
	}
};

const nameEditModalActive = () => {
	isNameEditModal.value = !isNameEditModal.value;
};

const time12 = () => {

	watch(isTime12, (newValue) => {
		localStorage.setItem("time12", String(newValue));
	});

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
						<button type="button" class="setting-btn" @click="nameEditModalActive">
							<font-awesome-icon :icon="['fas', 'caret-right']" />
						</button>
					</li>
					<li class="setting-item">
						<span class="setting-title"><label for="isTime12" @click="time12">12시간제</label></span>
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
				<div :class="isNameEditModal ? 'active' : ''" class="name-edit-modal">
					<div class="setting-header">
						<h4>이름 수정</h4>
						<button type="button" class="setting-btn" @click="nameEditModalActive">
							<font-awesome-icon :icon="['fas', 'caret-right']" />
						</button>
					</div>
					<div class="name-edit-modal-body">
						<label class="hidden" for="nameEdit">이름 수정</label>
						<div class="input-bottom-border">
							<input
								type="text"
								id="nameEdit"
								v-model="editName"
								name="nameEdit"
								placeholder="수정할 이름을 입력하세요."
								@keyup="nameEditEnter"
							>
							<span></span>
						</div>
						<button
							type="button"
							class="btn btn-round"
							@click="nameEdit"
						>수정
						</button>
						<p
							:class="[`${isSuccess ? 'input-info-success' : 'input-info-danger'}`,
						 `${isInfoVisible ? 'active' : ''}`]"
						>
							{{ formInfoMessage }}
						</p>
					</div>
				</div>
			</div>
		</template>
	</FloatModal>


</template>

<style>
@import "../../assets/css/setting.css";
</style>