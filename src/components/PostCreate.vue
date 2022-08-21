<template>
	<div class="row g-3">
		<div class="col col-2">
			<select
				class="form-select"
				v-model="type"
				aria-label="Default select example"
			>
				<option value="news">뉴스</option>
				<option value="notice">공지사항</option>
			</select>
		</div>
		<div class="col col-8">
			<input type="text" class="form-control" v-model="title" />
		</div>
		<div class="col col-2 d-grid">
			<button class="btn btn-primary" @click="createPost">추가</button>
		</div>
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	// emits: ['create-post'],
	// 객체 타입으로 선언할 경우 validation check 를 할 수 있다.
	emits: {
		createPost: newPost => {
			if (!newPost.type) return false;
			else if (!newPost.title) return false;
			return true;
		},
	},

	setup(props, context) {
		const title = ref('');
		const type = ref('news');

		const createPost = () => {
			const newPost = {
				type: type.value,
				title: title.value,
			};
			context.emit('createPost', newPost);
			type.value = 'news';
			title.value = '';
		};

		return {
			title,
			createPost,
			type,
		};
	},
};
</script>

<style lang="scss" scoped></style>
