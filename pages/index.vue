<template>
  <div>
    <div class="ad-box ad-left">
      <p>Reklam</p>
    </div>
    <div class="main-content">
      <div id="Baslik">
        <p>{{ questions[currentQuestionIndex].question }}</p>
        <hr id="Cizgi" />
      </div>
      <div id="Buton">
        <p id="Sorular">{{ currentQuestionIndex + 1 }} of {{ questions.length }} Questions</p>
        <div>
          <button
            id="Butonlar"
            v-for="(choice, index) in questions[currentQuestionIndex].choices"
            :key="index"
            @click="appendValue(choice)"
            :class="getButtonClass(choice)"
            :disabled="isDisabled"
          >
            {{ choice }}
          </button>
        </div>
      </div>
      <div>
        <button id="Next" @click="nextQuestion">
          {{ isLastQuestion ? "Finish the Quiz" : "Next Question" }}
        </button>
      </div>
      <div>
        <p id="Skor">
          Your Score: <p id="Sonuc">{{ score }} / {{ questions.length }}</p>
        </p>
      </div>
    </div>
    <div class="ad-box ad-right">
      <p>Reklam</p>
    </div>
  </div>
</template>

<script>

import "@/pages/index.css"

export default {
  name: "IndexPage",
  data() {
    return {
      questions: [
        {
          question: "Where is the capital of Turkey?",
          correctAnswer: "Ankara",
          choices: ["Istanbul", "Ankara", "Izmir", "Antalya", "Bursa"],
        },
        {
          question: "What is Earth's Secondary Planet",
          correctAnswer: "Moon",
          choices: ["Neptune", "Mars", "Moon", "Venus", "Mercury"],
        },
        {
          question: "Which is the largest ocean?",
          correctAnswer: "Pasific",
          choices: ["Indian", "Pasific", "Atlantic", "Arctic", "South"],
        },
      ],
      currentQuestionIndex: 0,
      selectedAnswer: "",
      score: 0,
    };
  },
  methods: {
    appendValue(choice) {
      this.selectedAnswer = choice;
    },
    getButtonClass(choice) {
      if (this.selectedAnswer === "") {
        return "";
      }
      if (choice === this.questions[this.currentQuestionIndex].correctAnswer) {
        return choice === this.selectedAnswer ? "correct-answer" : "correct";
      } else {
        return choice === this.selectedAnswer ? "incorrect" : "disabled";
      }
    },
    nextQuestion() {
      if (this.selectedAnswer === this.questions[this.currentQuestionIndex].correctAnswer) {
        this.score++;
      }
      if (this.currentQuestionIndex >= this.questions.length - 1) {
        alert(`Quiz Finished! Your Score: ${this.score}`);
        this.resetQuiz();
        return;
      }
      this.currentQuestionIndex++;
      this.selectedAnswer = "";
    },
    resetQuiz() {
      this.score = 0;
      this.currentQuestionIndex = 0;
      this.selectedAnswer = "";
    },
  },
  computed: {
    isDisabled() {
      return this.selectedAnswer !== "";
    },
  },
};
</script>
