/* eslint-disable */
<!-- 
	
	[ Component 관련해서는 Vue2.0과 비슷하다. ]
	- props
  - emit
	- provide & inject
  
  props & event branch참고
-->

<!-- 
  1. props
    - props: ['~~', '~~~'] 보다는 객체 타입으로 선언해주는 것을 권장한다.
      -> type: propsData의 타입 (Stringm, Number, Boolean, Array, Object ...)
      -> default: undefined를 전달 받을 경우 기본값
      -> required: 필수 여부
      -> validator: 유효성 검사
    - 전달받은 props 데이터를 setup() 에서 사용할 경우 setup(props) 로 선언해서 사용한다.
 -->
<script>
export default {
	props: {
		title: {
			type: String,
			required: true,
			default: '제목없음',
		},
		contents: {
			type: String,
			required: true,
		},
		isLike: {
			type: Boolean,
			default: false,
		},
	},
};
</script>

<!-- 
  2. emit
    - 자식 컴포넌트에서 부모 컴포넌트에게 이벤트를 발생시킬 때 사용한다.
    - Vue2때와는 다르게 this.$emit('이벤트명', parm) 으로 호출이 불가능
    - setup(props, context)에서 context.emit('이벤트명')으로 호출하고
      props:['속성명'] 처럼
      emits:['이벤트명'] or emit:{} 객체형으로 선언할 수 있다.
      객체형으로 사용할 경우 validation 체크가 가능하다.
 -->

<script>
export default {
	emits: ['toggle-like'],
	setup(props, context) {
		const toggleLike = () => {
			context.emit('toggle-like');
		};

		return {
			toggleLike,
		};
	},
};
</script>

<!-- 
  3. provide & inject
    - 부모 컴포넌트에서 자식 컴포넌트에게 데이터를 전달 할 경우 props 속성을 사용하지만
		  컴포넌트가 더 깊어지면 props를 사용하는데 한계가 있다. 이때, provide와 inject를 사용한다.
		- 하위 컴포넌트에 제공할 데이터는 상위 컴포넌트에서 setup() 부분에 provide('주입key', '주입value')  이렇게 선언한다.
 -->

<!-- 부모 컴포넌트 -->
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
		const count = ref(10);

		provide('static-message', staticMessage);
		provide('message', message);
		provide('count', count);
		return { count };
	},
};
</script>

<style lang="scss" scoped></style>

<!-- Deep자식 컴포넌트-->

<template>
	<div class="card">
		<div class="card-header">Deep Child Component</div>
		<div class="card-body">
			<p>staticMessage: {{ staticMessage }}</p>
			<p>message: {{ message }}</p>
			<p>count: {{ count }}</p>
		</div>
	</div>
</template>

<script>
import { inject } from 'vue';
export default {
	setup() {
		//inject의 두번째 param은 값이 없을경우 나오는 데이터이다.
		const staticMessage = inject('static-message', 'default message');
		const message = inject('message');
		const count = inject('count');
		return {
			staticMessage,
			message,
			count,
		};
	},
};
</script>

<style lang="scss" scoped></style>

/* eslint-enable */
