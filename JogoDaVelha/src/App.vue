
<template>
  <main class="pt-8 text-center dark:bg-gray-800 min-h-screen dark:text-white">
    <h1 class="mb-8 text-3xl font-bold uppercase">
      Jogo da Velha!
    </h1>

    <h3 class="text-xl mb-4"> Vez do {{ player }} jogar</h3>

    <div class="flex flex-col items-center mb-8">

      <div v-for="(row, x) in board"
        :key="x"
        class="flex"
      >
        <div 
          v-for="(cell, y) in row"
          :key="y"
          @click="MakeMove(x, y)"
          :class="`border border-white w-20 h-20 hover:bg-gray-700 flex items-center 
          justify-center material-icons-outlined text-4xl cursor-pointer `"  
          >
          {{ cell === 'X' ? 'close' : cell === 'O' ? 'circle' : '' }}
        </div>
      </div>

    </div>

    <h2 v-if="winner" class="text-6xl font-bold mb-8"> '{{ winner }}' Ganhaou </h2>

    <button
      @click="ResetGame"
      class="px-4 py-2 bg-purple-700 rounded-full uppercase font-bold hover:bg-pink-700 duration-300"
    >
    Resetar
  </button>

  </main>
</template>


<script setup>
  import { ref, computed } from 'vue'

  const player = ref('X');
  const board = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
  ])

  const CalculateWinner = (board) => {
  const lines = [[0, 1, 2],[3, 4, 5],[6, 7, 8],[0, 3, 6],[1, 4, 7],[2, 5, 8],[0, 4, 8],[2, 4, 6]]
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i]
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]
    }
  }
  return null
} 

  const winner = computed(() => CalculateWinner(board.value.flat()))

  const MakeMove = (x, y) => {
    if (winner.value) return

    if (board.value[x][y] !== '') return

    board.value[x][y] = player.value

    player.value = player.value === 'X' ? 'O' : 'X'
  }


  const ResetGame = () => {
    board.value = [
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ]
    player.value = 'X'
  }
</script>

<style>

</style>
