<template>
	<div>
		<div class="grid grid-cols-3 gap-4">
			<div v-for="month in 3" :key="month" class="border p-4">
				<h2 class="text-center text-2xl mb-5">{{ getMonthName(quarter, month) }}</h2>
				<div v-for="day in getDaysInMonth(quarter, month)" :key="day" class="mb-4">
					<span>{{ day }}</span>
					<i v-for="(icon, index) in icons" :key="icon" :class="['fa', `fa-${icon}`, 'text-lg', 'rounded-full', 'border', 'p-1', 'ml-1']"></i>
				</div>
			</div>
		</div>
		<div class="mt-5">
			<h2 class="text-center text-2xl mb-5">Legend</h2>
			<div class="flex flex-col items-center justify-center" v-for="(icon, index) in icons" :key="icon">
				<i :class="['fa', `fa-${icon}`, 'text-2xl']"></i>
				<span>{{ descriptions[index] }}</span>
			</div>
		</div>
		<div v-if="target" class="mt-5">
			<h2 class="text-center text-2xl mb-5">Quarter Target</h2>
			<p class="text-center">{{ target }}</p>
		</div>
		<button class="bg-teal-500 text-white px-4 py-2 mt-5 block mx-auto" @click="printCalendar">Print</button>
	</div>
</template>

<script setup lang="ts">

const props = defineProps<{
	quarter: number;
	icons: string[];
	descriptions: string[];
	target: string;
}>()

const { quarter, icons, descriptions, target } = props

const getMonthName = (quarter: number, month: number) => {
	const monthIndex = (quarter - 1) * 3 + month - 1
	const monthNames = [
		'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'
	]
	return monthNames[monthIndex]
}

const getDaysInMonth = (quarter: number, month: number) => {
	const monthIndex = (quarter - 1) * 3 + month - 1
	const date = new Date(new Date().getFullYear(), monthIndex + 1, 0)
	return date.getDate()
}

const printCalendar = () => {
	window.print()
}
</script>
