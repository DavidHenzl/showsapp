<script setup>
	import axios from 'axios'
	import { ref, watch } from 'vue';
	import Card from '@/components/Card.vue'

	const characters = ref(null)
	const page = ref(0)

	// const response = await axios.get("https://breakingbadapi.com/api/characters?limit=8")
	const response = await axios.get("http://localhost:8000/characters") // substitution (API server not working now)
	// characters.value = response.data
	characters.value = response.data.slice(0, 8) // substitution

	watch(page, async () => {
		// const res = await axios.get(`http://localhost:8000/characters?limit=8&offset=${page.value * 8}`)
		const res = (await axios.get(`http://localhost:8000/characters?`))
			.data.slice(8 * page.value, 8 * page.value + 8 ) // substitution
		// characters.value = res.data
		characters.value = res // substitution
		console.log(res)
	})
	

</script>

<template>
	<div class="container">
		<div class="cards">
			<Card
				v-for="character in characters"
				:key="character.char_id"
				:image="character.img"
				:name="character.name"
			>
				<div class="jobs">
					<p
						v-for="(job, index) in character.occupation"
						:key="job"
					>
						{{ job }}<span v-if="index < character.occupation.length - 1">,&nbsp</span>
					</p>
				</div>
			</Card>
		</div>
		<div class="button-container">
			<button @click="page--">&lt</button>
			<button @click="page++">></button>
		</div>
	</div>
</template>

<style scoped>
.container {
    background-color: rgb(27, 26, 26);
    padding: 30px;
}
.cards {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
    min-height: 700px;
}
.cards h3 {
    font-weight: bold;
}
.cards p {
    font-size: 10px;
}
.button-container {
    display: flex;
    justify-content: center;
    padding-top: 30px
}
.button-container button {
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    margin: 0 5px;
    cursor: pointer;
}
.spinner {
    display: flex;
    align-items: center;
    justify-content: center;
}

p {
    font-size: 10px;
}
.jobs {
    display: flex;
    flex-wrap: wrap;
}
</style>