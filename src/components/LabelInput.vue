<!-- emit을 v-model로 사용하기 ( 미완성 ) -->
<template>
	<label for="">
		이름
		<!-- <input type="text" v-model="username" /> -->
		<input
			type="text"
			:value="modelValue"
			@input="event => $emit('update:modelValue', event.target.value)"
		/>
	</label>
</template>

<script>
export default {
	props: ['modelValue'],
	emits: ['update:modelValue'],
	setup() {
		return {};
	},
};
</script>

<style lang="scss" scoped></style>
