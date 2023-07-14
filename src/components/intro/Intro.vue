<script setup>
import {ref} from "vue";

const {userName, isUserName} = defineProps({
	userName   : {
		type     : String,
		required : false,
	},
	isUserName : {
		type     : Boolean,
		required : true,
	},
});

const emit = defineEmits(["onUsername"]);

const name = ref("");

const setUserName = () => {
	emit("onUsername", name.value);
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