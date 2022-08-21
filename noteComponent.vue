/* eslint-disable */
<!-- 
	
	[ Component 관련해서는 Vue2.0과 비슷하다. ]
	- props
  - emit
  
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
/* eslint-enable */
