<script setup>
import RickAndMorty from './RickAndMorty.vue'
</script>

<template>
	<Suspense>
		<template #default>
			<RickAndMorty />
		</template>
		<template #fallback>
			<div class="cards">
				<img
					src="https://icaengineeringacademy.com/wp-content/uploads/2019/01/ajax-loading-gif-transparent-background-2.gif"
					alt="LOADING" />
			</div>
		</template>
	</Suspense>
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