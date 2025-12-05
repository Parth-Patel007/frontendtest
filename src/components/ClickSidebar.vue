<template>
  <div class="sidebar">
    <h2>Clicked Squares</h2>
    
    
    
    <div class="moves-container">
        <div
          v-for="(square, index) in clickedSquares"
          :key="`${square}-${index}`"
          class="square-item"
        >
          <span class="order">{{ index + 1 }}.</span>
          <span class="square">{{ square }}</span>
        </div>
    </div>
  </div>
</template>

<script setup>

defineProps({
  clickedSquares: {
    type: Array,
    required: true
  }
})
</script>

<style scoped>
.sidebar {
  width: 300px;
  background: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 20px;
}

h2 {

  font-size: 1.3rem;
  text-align: center;
}


.moves-container {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.square-item {
  display: flex;
  gap: 3px;
  padding: 8px 12px;
  background: #f5f5f5;
  border-radius: 4px;
  min-width: 60px;
}

.order {
  font-weight: bold;
}

.square {
  font-weight: bold;
}

@media (max-width: 767px) {
  .sidebar {
    width: 100%;
  }
}
</style>