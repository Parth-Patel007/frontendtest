<script setup>

const props = defineProps({
  highlightedSquares: {
    type: Set,
    required: true
  }
})

const emit = defineEmits(['square-clicked'])

const getSquareColor = (square) => {
  const row = Math.floor((square - 1) / 8)
  const col = (square - 1) % 8
  return (row + col) % 2 === 0 ? 'light' : 'dark'
}

const getSquareNotation = (index) => {
  const files = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'];
  const ranks = ['8', '7', '6', '5', '4', '3', '2', '1'];
    let row = Math.floor(index/8);
    let col = index % 8;
    

    return files[col] + ranks[row];
}

const isHighlighted = (notation) => {
  return props.highlightedSquares.has(notation)
}

const handleSquareClick = (notation) => {
    // console.log('Square clicked:', notation);
  emit('square-clicked', notation)
}
</script>

<template>
  <div class="chessboard-wrapper">
    <div class="chessboard">
      <div
        v-for="square in 64"
        :key="square"
        class="square"
        :class="[
          getSquareColor(square),
          { highlighted: isHighlighted(getSquareNotation(square-1)) }
        ]"
        @click="handleSquareClick(getSquareNotation(square-1))"
      >
        <span class="square_label">{{ getSquareNotation(square-1) }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.chessboard-wrapper {
  flex: 1;
}

.chessboard {
  width: 100%;
  aspect-ratio: 1;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  border: 2px solid #333;
}

.square {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.square.light {
  background-color: #EBECD0;
}

.square.dark {
  background-color: #739552;
}

.square:hover {
  opacity: 0.8;
}

.square.highlighted {
  background-color: #7fc97f;
}

.square_label {
  font-size: 1rem;
  color: black;
}

@media (max-width: 767px) {
  .chessboard-wrapper {
    max-width: 100%;
  }

  .square_label {
    font-size: 0.8rem;
  }

}
</style>

