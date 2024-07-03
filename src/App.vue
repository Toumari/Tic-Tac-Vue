<script setup>
import Player from './components/Player.vue';
import GameBoard from './components/GameBoard.vue';
import GameOver from './components/GameOver.vue';
import { ref } from 'vue';


const initialBoard = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', ''],
]);


function checkWinner(board, player) {
  // Check rows
  for (let row = 0; row < board.length; row++) {
    if (board[row][0] === player && board[row][1] === player && board[row][2] === player) {
      return true;
    }
  }

  // Check columns (similar logic)
  for (let col = 0; col < board[0].length; col++) {
    if (board[0][col] === player && board[1][col] === player && board[2][col] === player) {
      return true;
    }
  }

  // Check diagonals
  if (board[0][0] === player && board[1][1] === player && board[2][2] === player) {
    return true;
  }
  if (board[0][2] === player && board[1][1] === player && board[2][0] === player) {
    return true;
  }

  return false;
}

const board = ref(initialBoard);
const currentPlayer = ref('X');
const gameTurn = ref(0);
const winner = ref(false);
const isDraw = ref(false);

const handleCellClick = (row, col) => {
  if (board.value[row][col] !== '') {
    return;
  }

  board.value[row][col] = currentPlayer.value;
  gameTurn.value++;

  winner.value = checkWinner(board.value, currentPlayer.value);

  if (winner.value) {
    return;
  }

  if (gameTurn.value === 9 && !winner.value) {
    currentPlayer.value = 'Tie';
    isDraw.value = true;
    return;
  }

  if (!winner.value && currentPlayer.value === 'X') {
    currentPlayer.value = 'O';
  } else {
    currentPlayer.value = 'X';
  }
};

const handleRestart = () => {
  board.value = initialBoard.value.map(row => row.map(cell => ''));
  currentPlayer.value = 'X';
  gameTurn.value = 0;
  winner.value = false;
  isDraw.value = false;
};

</script>

<template>
  <div class="main">
    <h1 class="title">Tic-Tac-Vue</h1>
    <ol>
      <li>
        <Player player="Player 1" symbol="X" />
      </li>
      <li>
        <Player player="Player 2" symbol="O" />
      </li>
    </ol>
    <GameOver v-if="winner || isDraw" :isDraw="isDraw" :winner="currentPlayer" @onRestart="() => handleRestart()" />
    <GameBoard :board="board" @onCellClick="handleCellClick" />

  </div>
</template>


<style scoped>
.title {
  text-align: center;
  color: white;
  margin-top: 5rem;
  font-size: 3rem;
}

.main {
  position: relative;
}

ol {
  display: flex;
  justify-content: center;
  gap: 2rem;
  list-style-type: none;
  padding: 0;
}
</style>
