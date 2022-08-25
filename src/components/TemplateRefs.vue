<template>
	<div>
		<input type="text" ref="input" />
		<!-- input은 렌더링 이후에 값이 할당되기 때문에 v-if를 해주어야 오류가 안난다 -->
		<p v-if="input">{{ input.value }}, {{ $refs.input.value }}</p>
		<hr />
		<ul>
			<!-- ref를 string 값으로 선언 -->
			<!-- <li v-for="fruit in fruits" :key="fruit" ref="itemRefs">{{ fruit }}</li> -->

			<!-- ref를 function으로 선언 -->
			<li
				v-for="fruit in fruits"
				:key="fruit"
				:ref="el => itemRefs.push(el.textContent)"
			>
				{{ fruit }}
			</li>
		</ul>
	</div>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
	setup() {
		const input = ref(null);

		onMounted(() => {
			input.value.value = 'Hello World!!';
			console.log(input.value);

			// string으로 전달할 경우
			// itemRefs.value.forEach(item => {
			// 	console.log(item.textContent);
			// });

			//함수로 전달할 경우
			itemRefs.value.forEach(item => {
				console.log(item);
			});
		});

		const fruits = ref(['사과', '딸기', '포도']);
		const itemRefs = ref([]);
		return {
			input,
			fruits,
			itemRefs,
		};
	},
};
</script>

<style lang="scss" scoped></style>
