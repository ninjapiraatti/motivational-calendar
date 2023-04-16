<template>
	<div class="container mx-auto px-4">
	  <h3 class="text-center text-xl font-bold mb-6">Pick 3-5 icons:</h3>
	  <div class="icon-grid flex flex-wrap justify-center gap-4 mb-6">
		<div
		  v-for="(icon, index) in iconNames"
		  :key="index"
		  @click="selectIcon(icon)"
		  class="icon-wrapper flex items-center justify-center p-4 border border-gray-200 rounded cursor-pointer w-12 h-12"
		  :class="{ 'bg-teal-200': isSelected(icon) }"
		>
		  <font-awesome-icon :icon="['fas', icon]" class="icon" />
		</div>
	  </div>
	  <button
		@click="submitIcons"
		:disabled="selectedIcons.length < 3 || selectedIcons.length > 5"
		class="block mx-auto bg-teal-500 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
	  >
		Continue
	  </button>
	</div>
</template>


<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { library } from '@fortawesome/fontawesome-svg-core'
import { fas } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(fas)

const uniqueIconNames = new Set<string>()

Object.entries(fas)
	.filter(([key, value]) => key.startsWith("fa") && typeof value === "object")
	.forEach(([key, value]) => uniqueIconNames.add((value as any).iconName))

const iconNames = Array.from(uniqueIconNames)

const selectedIcons = ref<string[]>([])
const selectIcon = (icon: string) => {
	console.log(icon)
	if (selectedIcons.value.includes(icon)) {
		selectedIcons.value = selectedIcons.value.filter((i) => i !== icon)
	} else {
		selectedIcons.value.push(icon)
	}
}

const submitIcons = () => {
	emit('select', selectedIcons.value)
}

// Define emitted events
const emit = defineEmits(['select'])

onMounted(() => {
	console.log(fas)
})

const isSelected = (icon: string) => {
	return selectedIcons.value.includes(icon)
}
</script>
