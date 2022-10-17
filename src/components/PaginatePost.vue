<script setup>
defineProps(['inicioP','finP','limiteP'])
const emit=defineEmits(['nextP','prevP','bloqP','bloqN'])
</script>
<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      @click="emit('prevP')"
      type="button"
      class="btn btn-primary"
      :disabled="inicioP<=0"
    >
      Anterior
    </button>
    <button
      @click="emit('nextP')"
      type="button"
      class="btn btn-primary"
      :disabled="finP>=limiteP"
    >
      Siguiente
    </button>
  </div>
</template>
