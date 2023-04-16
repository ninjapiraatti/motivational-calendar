<template>
	<div>
		<h2 class="text-center text-2xl mb-5">Set an Optional Target</h2>
		<input v-model="inputTarget" type="text" class="border p-1 w-full" placeholder="Enter your target" />
		<button class="bg-teal-500 text-white px-4 py-2 mt-5 block mx-auto" @click="$emit('submit', inputTarget)">Continue</button>
	</div>
</template>


<script setup lang="ts">
import { ref } from 'vue'

const inputTarget = ref('')
</script>
