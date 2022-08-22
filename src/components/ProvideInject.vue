<template>
	<div class="container py-4">
		<div class="card">
			<div class="card-header">ProvideInject Component</div>
			<div class="card-body"><Child></Child></div>
			<button @click="count++">click</button>
		</div>
	</div>
</template>

<script>
import { provide, ref } from 'vue';
import Child from './Child.vue';
export default {
	components: {
		Child,
	},
	setup() {
		const staticMessage = 'static message';
		const message = ref('message');
		const updateMessage = newMessage => {
			message.value += newMessage;
		};
		const count = ref(10);

		provide('static-message', staticMessage);
		provide('message', { message, updateMessage });
		provide('count', count);
		return { count };
	},
};
</script>

<style lang="scss" scoped></style>
