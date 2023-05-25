<script setup>
  defineProps({
    init: Number,
    end: Number,
    maxLength: Number
  })
  const emit = defineEmits(['next', 'prev'])
</script>

<template>
  <div class="btn-group mb-2" role="group" aria-label="Basic example">
    <button 
      @click="emit('prev')" 
      type="button" 
      class="btn btn-outline-primary"
      :disabled="init <= 0"
    >
      Previus
    </button>
    <button 
      @click="emit('next')" 
      type="button" 
      class="btn btn-outline-primary"
      :disabled="end >= maxLength"
    >
      Next
    </button>
  </div>
  <h5>Post {{ init + 1 }} to {{ end }}</h5>
</template>
