<script setup>
import Time from "@/components/time/Time.vue";
import Todo from "@/components/todo/Todo.vue";
import Intoro from "@/components/intro/Intro.vue";
import Setting from "@/components/setting/Setting.vue";
import {onMounted, ref} from "vue";

const localStorageUserName = localStorage.getItem("userName");
const isSuccess = ref(false);
const isUserName = ref(true);
const isInfoVisible = ref(false);
const userName = ref("");
const formInfoMessage = ref("");

onMounted(() => {
	if (localStorageUserName !== null) {
		userName.value = localStorageUserName;
		isUserName.value = false;
	}

	if (localStorage.getItem("time12") === null) {
		localStorage.setItem("time12", "false");
	}
});

const setUserName = (value) => {
	if (value === "") {
		alert("이름을 입력하세요");
		return false;
	}
	localStorage.setItem("userName", value);
	userName.value = value;

	isUserName.value = false;
};

const visibleTimeout = () => {
	setTimeout(() => {
		isInfoVisible.value = false;
	}, 5000);
};

const nameEdit = (value) => {
	isInfoVisible.value = true;

	if (value !== "") {
		isSuccess.value = true;
		formInfoMessage.value = "수정 되었습니다.";
		localStorage.setItem("userName", value);
		userName.value = value;

		visibleTimeout();
	} else {
		isSuccess.value = false;
		formInfoMessage.value = "이름을 입력해주세요.";

		visibleTimeout();
	}
};
</script>

<template>
	<div
		class="background"
		style="background-image: url('/src/assets/images/ocean-1867285_1280.jpg')"
	>
		<Time />
		<Intoro :isUserName="isUserName" :userName="userName" @onUsername="setUserName" />
		<div class="tmp">

		</div>
		<Todo />
		<Setting
			:formInfoMessage="formInfoMessage"
			:isInfoVisible="isInfoVisible"
			:isSuccess="isSuccess"
			@onNameEdit="nameEdit"
		/>
	</div>
</template>

<style scoped>
@import "../../src/assets/css/home.css";

/*.tmp {
	width: 100%;
	min-height: 30vh;
}*/
</style>