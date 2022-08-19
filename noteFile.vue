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
import { onBeforeMount, onMounted, ref } from 'vue';
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

<!-- 
	[ CompositonAPI의 Reactive ]
  - API의 성격에 따라 아래와 같이 나뉘어진다.
	0. setup()
	  * 가장 빠른 시점 으로 첫번째 인자로 props, 두번째 인자로 context가 온다.
	1. Reactivity API ( 반응형 API)
	   * ref(), reactive(), reactive state(반응상태), computed, state(계산된상태), watchers(감시자) 등...
	2. Lifecycle Hooks
	   * onMounted(), onUnmounted() 등...
	3. D/I 
		 * provide(), inject() 등 ...
	
	-->

<!-- 1.1 ref -->

<template>
	<div>Hello Vue3</div>
	<h2>반응형 메시지</h2>
	<!-- 변경 가능 -->
	<p>{{ reactiveMessage }}</p>
	<button @click="addReactiveMessage">Add Message</button>

	<h2>일반 메시지</h2>
	<!-- 변경 불가능 -->
	<p>{{ normalMessage }}</p>
	<button @click="addNormalMessage">Add Message</button>
</template>

<script>
import { isRef, ref } from 'vue'; // import 필수

export default {
	setup() {
		// setup()에서 선언한 값들은 return 해줘야 사용가능하다.
		console.log('setup()');

		const reactiveMessage = ref('Hello Reactive Message'); //반응형 객체로 만들어 준 것이다. reactiveMessage.value로 접근
		const addReactiveMessage = () => {
			reactiveMessage.value = reactiveMessage.value + '!';
		};

		let normalMessage = 'Hello Reactive Message'; // 정적인 변수이므로 변경이 불가능
		const addNormalMessage = () => {
			normalMessage = normalMessage + '!';
		};

		console.log(isRef(reactiveMessage)); // 반응형 객체인지를 확인

		onMounted(() => {
			console.log('onMounted');
		});

		onBeforeMount(() => {
			console.log('onBeforeMounted');
		});

		return {
			reactiveMessage,
			normalMessage,
			addReactiveMessage,
			addNormalMessage,
		};
	},
};
</script>
<style scoped></style>

<!-- 
	1.2 reactive()
	  - ref()로 선언할 수 있지만 reactive로도 선언이 가능하다.

 -->

/* eslint-enable */
