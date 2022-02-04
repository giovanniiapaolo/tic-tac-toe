<template>
	<div>
		<h1>TIC TAC TOE</h1>
		<table>
			<tr>
				<td @click="turn(0, 0)">{{ board[0][0].val }}</td>
				<td @click="turn(0, 1)">{{ board[0][1].val }}</td>
				<td @click="turn(0, 2)">{{ board[0][2].val }}</td>
			</tr>
			<tr>
				<td @click="turn(1, 0)">{{ board[1][0].val }}</td>
				<td @click="turn(1, 1)">{{ board[1][1].val }}</td>
				<td @click="turn(1, 2)">{{ board[1][2].val }}</td>
			</tr>
			<tr>
				<td @click="turn(2, 0)">{{ board[2][0].val }}</td>
				<td @click="turn(2, 1)">{{ board[2][1].val }}</td>
				<td @click="turn(2, 2)">{{ board[2][2].val }}</td>
			</tr>
		</table>

		<h3 v-if="!endOfGame">Player {{ player }}'s turn</h3>
		<h3 v-else-if="endOfGame == 'X'">Player X, WON!</h3>
		<h3 v-else-if="endOfGame == 'O'">Player O, WON!</h3>
		<h3 v-else>DRAW</h3>
	</div>
</template>

<script>
export default {
	data() {
		return {
			player: 'X',
			movesLeft: 9,
			board: {
				0: {
					0: { val: '', locked: false },
					1: { val: '', locked: false },
					2: { val: '', locked: false },
				},
				1: {
					0: { val: '', locked: false },
					1: { val: '', locked: false },
					2: { val: '', locked: false },
				},
				2: {
					0: { val: '', locked: false },
					1: { val: '', locked: false },
					2: { val: '', locked: false },
				},
			},
		};
	},
	methods: {
		turn(i, j) {
			if (this.board[i][j].locked) {
				return;
			}
			if (this.endOfGame) {
				return;
			}
			this.board[i][j].val = this.player;
			this.player === 'O' ? (this.player = 'X') : (this.player = 'O');
			this.board[i][j].locked = true;
			this.movesLeft--;
		},

		eq(i, j, player) {
			return this.board[i][j].val === player;
		},
	},

	computed: {
		endOfGame() {
			for (const t of ['X', 'O']) {
				for (const i in this.board) {
					if (
						this.eq(i, 0, t) &&
						this.eq(i, 1, t) &&
						this.eq(i, 2, t)
					)
						return t;
					if (
						this.eq(0, i, t) &&
						this.eq(1, i, t) &&
						this.eq(2, i, t)
					)
						return t;
				}
				if (this.eq(0, 0, t) && this.eq(1, 1, t) && this.eq(2, 2, t))
					return t;
				if (this.eq(0, 2, t) && this.eq(1, 1, t) && this.eq(2, 0, t))
					return t;
			}
			if (this.movesLeft == 0) {
				return 'DRAW';
			}
			return '';
		},
	},
};
</script>

<style scoped>
table {
	margin: 0 auto;
	table-layout: fixed;
	white-space: nowrap;
	border-collapse: collapse;
	border-style: hidden;
}
table td {
	border: 3px solid #4c566a;
	font-size: 36px;
	table-layout: fixed;
	width: 7rem;
	height: 7rem;
}
</style>
