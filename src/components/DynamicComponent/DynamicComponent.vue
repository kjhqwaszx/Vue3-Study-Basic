<template>
	<div class="container py-4">
		<button
			class="btn btn-primary me-2"
			@click="changeCurrentComp(DynamicApple)"
		>
			사과
		</button>
		<button class="btn btn-danger" @click="changeCurrentComp(DynamicBanana)">
			바나나
		</button>
		<hr />

		<component :is="currentComp"></component>
	</div>
</template>

<script setup>
import { shallowRef } from 'vue';
import DynamicApple from './DynamicApple.vue';
import DynamicBanana from './DynamicBanana.vue';

// :is 속성으로 컴포넌트를 넘길때에는 ref 보다 shallowRef가 성능적으로 유리하다.
// const currentComp = ref(DynamicApple);
const currentComp = shallowRef(DynamicApple);
const changeCurrentComp = comp => (currentComp.value = comp);
</script>

<style lang="scss" scoped></style>
