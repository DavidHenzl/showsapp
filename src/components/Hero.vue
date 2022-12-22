<script setup>
	const props = defineProps(['isBreakingBad'])

	const emit = defineEmits(['selectShow'])

</script>

<template>
	<div class="hero">
		<h1>{{ isBreakingBad ? 'Breaking Bad' : 'Rick and Morty' }}</h1>
		<p @click="emit('selectShow')">{{ isBreakingBad ? 'Rick and Morty' : 'Breaking Bad' }}</p>
	</div>
</template>

<style scoped>
	.hero {
    height : 40vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    flex-direction: column
	}
	.hero img {
			position: absolute;
			height: 700px;
			opacity: 0.1;
	}
	.hero h1 {
			font-size: 100px;
			font-weight: bold;
	}
	.hero p {
			cursor: pointer;
	}
</style>