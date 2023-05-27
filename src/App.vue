<template>
	<div class="container mx-auto min-h-screen px-4 py-10 bg-gradient-to-br from-yellow-50 to-yellow-100">
		<transition name="fade">
			<QuarterPicker v-if="step === 1" @select="setQuarter" />
			<IconPicker v-else-if="step === 2" @select="setIcons" />
			<IconDescription :icons="icons" v-else-if="step === 3" @submit="setDescriptions" />
			<TargetInput v-else-if="step === 4" @submit="setTarget" />
			<Calendar v-else :quarter="quarter" :icons="icons" :descriptions="descriptions" :target="target" />
		</transition>
	</div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import QuarterPicker from './components/QuarterPicker.vue'
import IconPicker from './components/IconPicker.vue'
import IconDescription from './components/IconDescription.vue'
import TargetInput from './components/TargetInput.vue'
import Calendar from './components/Calendar.vue'

const step = ref(1)
const quarter = ref(0)
const icons = ref<string[]>([])
const descriptions = ref<string[]>([])
const target = ref('')

const setQuarter = (q: number) => {
	quarter.value = q
	step.value = 2
}

const setIcons = (selectedIcons: string[]) => {
	icons.value = selectedIcons
	step.value = 3
}

const setDescriptions = (desc: string[]) => {
	descriptions.value = desc
	step.value = 4
}

const setTarget = (t: string) => {
	target.value = t
	step.value = 5
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
	opacity: 0;
}
</style>
