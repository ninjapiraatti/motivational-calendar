<template>
	<div class="container mx-auto px-4">
		<h2 class="text-center text-2xl mb-5">Describe Your Icons</h2>
		<div v-for="(icon, index) in icons" :key="icon" class="mb-4 flex items-center">
			<i :class="['fa', `fa-${icon}`, 'text-2xl']"></i>
			<input v-model="descriptions[index]" type="text" class="border ml-4 p-1 flex-grow" placeholder="Description" />
		</div>
		<button
			@click="$emit('submit', descriptions)"
			class="bg-teal-500 text-white px-4 py-2 mt-5 block mx-auto"
		>
			Continue
		</button>
	</div>
</template>


<script setup lang="ts">
import { ref, watchEffect, onMounted } from 'vue'

const props = defineProps<{
	icons: string[];
}>()

const { icons } = props
const descriptions = ref<string[]>([])

watchEffect(() => {
	if (icons) {
		descriptions.value = new Array(icons.length).fill('')
	}
})

onMounted(() => {
	console.log(icons)
})
</script>
