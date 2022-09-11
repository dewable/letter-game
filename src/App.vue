<template>
	<div class="header">
		<h2>Letter Game</h2>
		<h3>By: Brian Carrington | <a target="_blank" href="https://github.com/dewable/letter-game">Code</a></h3>
	</div>
	<div class="game">
		<letter-game/>
	</div>
</template>

<script>
	import LetterGame from './components/LetterGame';


	export default {
		name: 'App',
		components: {
			LetterGame
		}
	}
</script>

<style scoped>
	.header {
		text-align: center;
	}
	.game {
		border-style: outset;
		text-align: center;
	}
</style>
