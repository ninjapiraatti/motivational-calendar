<template>
	<div>
		<div class="grid grid-cols-3 gap-4">
			<div v-for="month in 3" :key="month" class="p-4">
				<h2 class="mb-2">{{ getMonthName(quarter, month) }}</h2>
				<div v-for="day in getDaysInMonth(quarter, month)" :key="day" class="mb-1 text-xs flex items-center">
					<span>{{ day.toString().padStart(2, '0') }}.</span>
					<i v-for="(icon, index) in icons" :key="icon" :class="['icon', 'fa', `fa-${icon}`, 'rounded-full', 'border', 'pr-1', 'ml-1']"></i>
				</div>
			</div>
		</div>
		<div class="mt-2">
			<div class="flex flex-col items-center justify-center" v-for="(icon, index) in icons" :key="icon">
				<div>
					<i :class="['fa', `fa-${icon}`, 'text-sm', 'mr-2']"></i>
					<span class="text-sm">{{ descriptions[index] }}</span>
				</div>
			</div>
		</div>
		<div v-if="target" class="mt-2">
			<p class="text-center">{{ target }}</p>
		</div>
		<button class="bg-teal-500 text-white px-4 py-2 mt-5 block mx-auto print-none" @click="printCalendar">Print</button>
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

<style scoped>
.icon {
	width: 15px;
	height: 15px;
	border-color: #888;
	border-width: 0.5px;
	color: #bbb;
	background-color: #eee;
	overflow: hidden;
	font-size: 0.5rem;
	line-height: 1.5;
}
.icon::before {
	padding-left: 1.5px;
}
</style>

