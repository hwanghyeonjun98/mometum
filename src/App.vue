<script setup>
import Time from "@/components/Time.vue";
</script>

<template>
	<div class="background">
		<Time />

		<div class="todo-area">
			<form id="todo-form" action="#" @submit.prevent>
				<input type="text" id="todo" name="todo" placeholder="오늘 할일을 입력하세요." />
				<button type="submit" data-submit="">추가</button>
			</form>

			<ul class="todo-list">
				<li class="todo">
					<div class="todo-content">
						<div class="todo-checkbox">
							<input type="checkbox" id="todo-check" name="todo">
						</div>
						<p class="todo-text">
							<label for="todo">오늘 할일</label>
						</p>
					</div>
					<div class="delete">
						<button type="button">삭제</button>
					</div>
				</li>
			</ul>

			<div class="bible">
				<p class="bible-content"></p>
				<p class="bible-verse"></p>
			</div>
		</div>
	</div>
</template>

<style scoped>

</style>
