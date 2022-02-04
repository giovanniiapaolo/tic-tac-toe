<template>
	<div id="app">
		<game />
	</div>
</template>

<script>
import game from './components/game.vue';

export default {
	name: 'app',
	components: {
		game,
	},
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Rubik');
#app {
	font-family: 'Rubik', 'Courier New', Courier, monospace;
	line-height: 1.5;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #434c5e;
	margin-top: 60px;
}
</style>
