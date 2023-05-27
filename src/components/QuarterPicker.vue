<template>
	<div>
		<h2 class="text-center text-2xl mb-5">Choose a Quarter</h2>
		<div class="flex justify-center">
			<button v-for="i in 4" :key="i" class="bg-teal-500 text-white px-4 py-2 m-2" @click="$emit('select', i)">
				{{ i }}
			</button>
		</div>
	</div>
</template>


<script setup lang="ts"></script>
