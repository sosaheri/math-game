<template>
  <input type="number" v-model="userAnswer" />
  <button @click="$emit('submit', userAnswer)">Enviar</button>
</template>

<script>
export default {
  data() {
    return {
      userAnswer: ''
    }
  }
}
</script>