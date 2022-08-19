<template>
	<div>
		<button @click="increment1">Click : {{ state.count }}</button>
		<button @click="increment2">Click : {{ state.deep1.count }}</button>
	</div>
</template>

<script>
import { reactive } from 'vue';

export default {
	setup() {
		const state = reactive({
			count: 0,
			deep1: {
				count: 0,
			},
		});

		const increment1 = () => {
			state.count++;
		};
		const increment2 = () => {
			state.deep1.count++;
		};

		return {
			state,
			increment1,
			increment2,
		};
	},
};
</script>

<style lang="scss" scoped></style>
