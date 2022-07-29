<script setup lang="ts">
import QuoteVue from './components/Quote.vue';
</script>

<template>
	<main>
		<h1>Programmer Quotes</h1>
		<QuoteVue />
	</main>
</template>

<style scoped>
main {
	display: flex;
	flex-direction: column;
}

h1 {
	color: #FAFFFD;
	align-self: center;
}
</style>
