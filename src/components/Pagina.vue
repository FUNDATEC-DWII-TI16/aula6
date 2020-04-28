<template>
	<div class="pagina container-fluid">
		<div class="row">
			<div class="col-6 conteudo">
				<click-counter></click-counter>
			</div>
			<div class="col-6 conteudo">
				<tic-tac-toe></tic-tac-toe>
			</div>
		</div>
	</div>
</template>

<script>
import ClickCounter from "./ClickCounter.vue";
import TicTacToe from "./TicTacToe.vue";

export default {
	components: {
		ClickCounter,
		TicTacToe,
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
