<template>
	<div class="tic-tac-toe">
		<div>Jogador da vez: {{ jogadorDaVez }}</div>
		<div class="row">
			<div class="col-4 field border-bottom border-right" @click="gravarJogada(0)">{{ jogadas[0] }}</div>
			<div class="col-4 field border-bottom" @click="gravarJogada(1)">{{ jogadas[1] }}</div>
			<div class="col-4 field border-bottom border-left" @click="gravarJogada(2)">{{ jogadas[2] }}</div>
		</div>
		<div class="row">
			<div class="col-4 field border-right" @click="gravarJogada(3)">{{ jogadas[3] }}</div>
			<div class="col-4 field" @click="gravarJogada(4)">{{ jogadas[4] }}</div>
			<div class="col-4 field border-left" @click="gravarJogada(5)">{{ jogadas[5] }}</div>
		</div>
		<div class="row">
			<div class="col-4 field border-top border-right" @click="gravarJogada(6)">{{ jogadas[6] }}</div>
			<div class="col-4 field border-top" @click="gravarJogada(7)">{{ jogadas[7] }}</div>
			<div class="col-4 field border-top border-left" @click="gravarJogada(8)">{{ jogadas[8] }}</div>
		</div>
		{{ resultado }}
	</div>
</template>

<script>
export default {
	data() {
		return {
			jogadas: [null, null, null, null, null, null, null, null, null],
			jogadasX: [],
			jogadasO: [],
			jogadorDaVez: "X",
			resultado: null,
		};
	},
	methods: {
		gravarJogada(posicao) {
			if (this.jogadas[posicao] !== null) return;

			this.jogadas[posicao] = this.jogadorDaVez;
			let jogadasDoJogador = this.jogadorDaVez === "X" ? this.jogadasX : this.jogadasO;
			jogadasDoJogador.push(posicao);

			if (this.possuiGanhador()) {
				this.resultado = `Ganhador: ${this.jogadorDaVez}`;
				return;
			}

			if (this.jogadas.filter((j) => j === null).length === 0) {
				this.resultado = `Ninguém ganhou!`;
				return;
			}

			this.trocarJogador();
		},
		trocarJogador() {
			if (this.jogadorDaVez === "X") this.jogadorDaVez = "O";
			else this.jogadorDaVez = "X";
		},
		possuiGanhador() {
			//horizontais
			const h1 = [0, 1, 2];
			const h2 = [3, 4, 5];
			const h3 = [6, 7, 8];

			const v1 = [0, 3, 6];
			const v2 = [1, 4, 7];
			const v3 = [2, 5, 8];

			const d1 = [0, 4, 8];
			const d2 = [2, 4, 6];

			const combinacoesGanhadores = [h1, h2, h3, v1, v2, v3, d1, d2];

			let jogadasParaAvaliar = this.jogadorDaVez === "X" ? this.jogadasX : this.jogadasO;

			let combinacoesGanhadoresDoJogador = combinacoesGanhadores.filter((combinacao) => {
				if (jogadasParaAvaliar.includes(combinacao[0]) && jogadasParaAvaliar.includes(combinacao[1]) && jogadasParaAvaliar.includes(combinacao[2]))
					return true;

				return false;
			});

			if (combinacoesGanhadoresDoJogador.length > 0) return true;
			return false;
		},
	},
};
</script>

<style scoped>
.tic-tac-toe {
	width: 100%;
	height: 300px;
}

.field {
	height: 100px;
	font-size: 32dp;
	cursor: pointer;
	vertical-align: middle;
	padding-top: auto;
	padding-bottom: auto;
}
</style>
