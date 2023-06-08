<script setup>
import axios from 'axios'
import { ref, watch, onMounted } from 'vue'
import Card from './Card.vue'

const characters = ref(null)
const page = ref(1)
const numberOfCharacters = ref(0)

onMounted(async () => {
	const response = await axios.get('https://swapi.dev/api/people')
	characters.value = response.data.results
	numberOfCharacters.value = response.data.count
})

watch(page, async () => {
	const res = await axios.get(`https://swapi.dev/api/people/?page=${page.value}`)
	characters.value = res.data.results
})

const decreasePage = () => {
	if (page.value > 1) {
		page.value--
	}
}

const increasePage = () => {
	if (page.value * 10 < numberOfCharacters.value) {
		page.value++
	}
}

</script>

<template>
	<div class="container">
		<div v-if="characters" class="cards">
			<Card
				v-for="character in characters"
				:key="character.id"
				image="https://www.cardcentral.co.nz/wp-content/uploads/2018/11/26-Star-Wars-logo-black-5x6.jpg"
				:name="character.name"
			>
				<p>Year: {{ character.birth_year }}</p>
			</Card>
		</div>
		<div v-else class="cards spinner">
			<img src="https://icaengineeringacademy.com/wp-content/uploads/2019/01/ajax-loading-gif-transparent-background-2.gif" alt="LOADING">
		</div>
		<div class="button-container">
			<button @click="decreasePage">&lt</button>
			<button @click="increasePage">></button>
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
	padding-top: 30px;
}
.button-container button {
	border: none;
	width: 50px;
	height: 50px;
	border-radius: 100%;
	margin: 0 5px;
	cursor: pointer;
	color: white;
	font-weight: bold;
	background-color: rgb(245, 50, 50);
}

.spinner {
	display: flex;
	align-items: center;
	justify-content: center;
}
</style>
