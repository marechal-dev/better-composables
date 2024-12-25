<script setup lang="ts">
import { ref } from 'vue';
import { useMouse } from './composables/mouse';
import { useTitle, useRefHistory } from '@vueuse/core';

const { x, y } = useMouse();
const title = useTitle('Green Socks', {
	titleTemplate: '%s | My Store'
})

const counter = ref(0);
const { undo } = useRefHistory(counter, {
	deep: true,
});

counter.value++;

console.log(counter.value);

function undoRef() {
	undo();
	console.log(counter.value);
}
</script>

<template>
  <div class="col">
		<span>Mouse X: {{ x }}</span>
		<span>Mouse Y: {{ y }}</span>
		<button @click="undoRef">Click</button>
	</div>
</template>

<style scoped>
.col {
	display: flex;
	flex-direction: column;
	align-items: center;
}
</style>
