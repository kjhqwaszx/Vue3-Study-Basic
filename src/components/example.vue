<template>
	<div>
		<main>
			<div class="container py-4">
				<FancyButton>click!!</FancyButton>
				<hr class="my-4" />
				<AppCard>
					<template v-slot:header> 제목 입니다.</template>
					<template v-slot:default> 내용 입니다.</template
					><template v-slot:footer> 푸터 입니다.</template>
				</AppCard>
			</div>
		</main>
	</div>
</template>

<script>
import { reactive, ref } from 'vue';
import FancyButton from './FancyButton.vue';
import AppCard from './AppCard.vue';

export default {
	components: {
		FancyButton,
		AppCard,
	},
	setup() {
		const posts = reactive([
			{ id: 1, title: '제목1', contents: '내용1', isLike: true, type: 'news' },
			{ id: 2, title: '제목2', contents: '내용2', isLike: true, type: 'news' },
			{ id: 3, title: '제목3', contents: '내용3', isLike: true, type: 'news' },
			{
				id: 4,
				title: '제목4',
				contents: '내용4',
				isLike: false,
				type: 'notice',
			},
			{
				id: 5,
				title: '제목5',
				contents: '내용5',
				isLike: false,
				type: 'notice',
			},
		]);

		const createPost = newPost => {
			console.log('create-post', newPost);
			posts.push(newPost);
		};

		const username = ref('');

		return {
			posts,
			createPost,
			username,
		};
	},
};
</script>

<style lang="scss" scoped></style>
