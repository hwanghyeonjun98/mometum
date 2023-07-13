<script setup>
import {onMounted, ref} from "vue";

const localStorageUserName = localStorage.getItem("userName");
const userName = ref("");
const name = ref("");

const isUserName = ref(true);

onMounted(() => {
	if (localStorageUserName !== null) {
		userName.value = localStorageUserName;
		isUserName.value = false;
	}
});

const setUserName = () => {
	if (name.value === "") {
		alert("이름을 입력하세요");
		return false;
	}
	localStorage.setItem("userName", name.value);
	userName.value = name.value;
	name.value = "";

	isUserName.value = false;
};
</script>

<template>
	<div class="intro">
		<div v-if="isUserName" class="set-user-form">
			<input type="text" id="name" v-model="name" autocomplete="off" name="name" placeholder="이름을 입력하세요.">
			<button type="button" @click="setUserName">입력</button>
		</div>
		<ul v-else class="user">
			<li>
				<p class="text-capitalize">hello! </p>
			</li>
			<li>
				<span id="userName">{{ userName }}</span>
			</li>
		</ul>
	</div>
</template>

<style>
@import "../../assets/css/intro.css";
</style>