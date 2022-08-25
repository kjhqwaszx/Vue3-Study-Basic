<template>
	<div class="container py-4">
		{{ msg }}
		<br />
		{{ message }}
		<button @click="sayHello">click</button>
		<!-- <PostItem
			type="news"
			title="제목"
			contents="내용"
			:is-like="true"
		></PostItem> -->

		<SetupPostItem
			type="news"
			title="제목"
			contents="내용"
			:is-like="true"
		></SetupPostItem>
	</div>
</template>

<script setup>
import { ref } from 'vue';
// import PostItem from '@/components/setup/PostItem.vue';
import SetupPostItem from '@/components/setup/SetupPostItem.vue';

const msg = 'Hello World!!';
const message = ref('');
const sayHello = () => alert('Hello');
</script>

<style lang="scss" scoped></style>
