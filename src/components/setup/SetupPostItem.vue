<template>
	<div class="card">
		<div class="card-body">
			<!-- type: news, notice -->
			<span class="badge bg-secondary">
				{{ typeName }}
			</span>
			<h5 class="card-title red" mt-2>{{ title }}</h5>
			<p class="card-text">
				{{ contents }}
			</p>
			<a ref="" href="#" :class="isLikeClass" @click="toggleLike">좋아요</a>
		</div>
	</div>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
	type: {
		type: String,
		default: 'news',
		validator: value => {
			return ['news', 'notice'].includes(value);
		},
	},
	title: {
		type: String,
		required: true,
	},
	contents: {
		type: String,
		// required: true,
	},
	isLike: {
		type: Boolean,
		default: false,
	},
});

const emit = defineEmits(['toggle-like']);

const isLikeClass = computed(() =>
	props.isLike ? 'btn btn-danger' : 'btn btn-outline-danger',
);

const typeName = computed(() => (props.type === 'news' ? '뉴스' : '공지사항'));

const toggleLike = () => {
	emit('toggle-like');
};
</script>

<style scoped></style>
