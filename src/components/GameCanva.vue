<template>
  <div>
    <h1>Juego de Matemáticas</h1>
    <MathQuestion :numbers="numbers" :operation="operation" />
    <AnswerInput @submit="checkAnswer" />
    <p>Puntaje: {{ score }}</p>
  </div>
</template>

<script>
import MathQuestion from './MathQuestion.vue'
import AnswerInput from './AnswerInput.vue'

export default {
  components: {
    MathQuestion,
    AnswerInput
  },
  data() {
    return {
      numbers: [],
      operation: '',
      score: 0,
      level: 1,
      maxNumber: 10 // Ajusta el rango de números según el nivel
    }
  },
  methods: {
    generateQuestion() {
      // Genera dos números aleatorios entre 1 y maxNumber
      const num1 = Math.floor(Math.random() * this.maxNumber) + 1;
      const num2 = Math.floor(Math.random() * this.maxNumber) + 1;

      // Selecciona una operación aleatoria
      const operations = ['+', '-', '*'];
      const operation = operations[Math.floor(Math.random() * operations.length)];

      this.numbers = [num1, num2];
      this.operation = operation;
    },
    checkAnswer(userAnswer) {
      const correctAnswer = eval(`${this.numbers[0]} ${this.operation} ${this.numbers[1]}`);
      if (userAnswer === correctAnswer) {
        this.score++;
        this.generateQuestion();
      } else {
        this.score--;
      }
    },
    // Método para subir de nivel
    levelUp() {
      this.level++;
      this.maxNumber *= 2; // Dobla el rango de números
    }
  },
  created() {
    this.generateQuestion();
  }
}
</script>