/* eslint-disable */

<!-- 
	
	[ Options API vs Composition API ]
	- Composition API는 옵션(data, methods, ... )을 선언하는 대신 가져온 함수(ref, onMounted, ...)를 사용하여 Vue 컴포넌트를 작성할 수 있는 API 세트를 말한다.
	- 기존의 Options은 data 선언부, methods 선언부가 나눠져 있어 해당 data를 처리하는 로직을 찾기가 쉽지 않다 ( 스크롤링을 계속 해야함 ), 하지만 Composition는 그럴 필요가 없다. 
	  * 데이터 선언, 처리 로직이 모여있기 때문에 유틸이나 모듈로 빼 재사용하기 편하다. ( Composable 함수 라고 부름) -> Mixin의 모든 단점을 해결

		-->

<!-- Optionsal -->

<template>
	<div>
		<button v-on:click="increment">Counter: {{ counter }}</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			counter: 0,
		};
	},
	methods: {
		increment() {
			this.counter++;
		},
	},
	mounted() {
		console.log('컴포넌트가 마운트 되었습니다!');
	},
};
</script>

<style lang="scss" scoped></style>

<!-- Composition -->

<template>
	<div>
		<button v-on:click="increment">Counter: {{ counter }}</button>
	</div>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
	setup() {
		const counter = ref(0);
		const increment = () => counter.value++;
		onMounted(() => {
			console.log('컴포넌트가 마운트 되었습니다!');
		});
		return {
			counter,
			increment,
		};
	},
};
</script>

<style lang="scss" scoped></style>
