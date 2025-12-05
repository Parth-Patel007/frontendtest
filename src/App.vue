<script setup>
import { ref } from 'vue'
import ChessBoard from './components/ChessBoard.vue'
import ClickSidebar from './components/ClickSidebar.vue'

const highlightedSquares = ref(new Set())
const clickHistory = ref([])

const handleSquareClick = (square) => {
  if (!highlightedSquares.value.has(square)) {
    highlightedSquares.value.add(square)
    clickHistory.value.push(square)
  }
}
</script>

<template>
  <div class="app-container">
    <h1>Chess.com Frontend Challenge</h1>
    <div class="chess-layout">
      <ChessBoard 
        :highlighted-squares="highlightedSquares"
        @square-clicked="handleSquareClick"
      />
      <ClickSidebar 
        :clicked-squares="clickHistory"
      />
    </div>
  </div>
</template>

<style scoped>
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}

.chess-layout {
  display: flex;
  justify-content: space-around;
  gap: 20px;
}

@media (max-width: 767px) {
  .chess-layout {
    flex-direction: column;
  }
}
</style>