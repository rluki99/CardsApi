<script setup>
import { ref } from 'vue';
import Hero from './components/Hero.vue';
import RickAndMortySuspense from './components/RickAndMortySuspense.vue'
import StarWars from './components/StarWars.vue'

const isRickAndMorty = ref(true)
</script>

<template>
	<main>
		<Hero :isRickAndMorty="isRickAndMorty" @selectShow="isRickAndMorty = !isRickAndMorty"/>
    <KeepAlive>
      <Component :is="isRickAndMorty ? RickAndMortySuspense : StarWars"/>
    </KeepAlive>
	</main>
</template>

<style scoped>
.cards {
  height: 700px;
  background-color: rgb(27, 26, 26);
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>