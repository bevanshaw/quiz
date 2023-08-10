<script setup>
import { ref } from "vue";
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";
const data = ref({
  questions: [
    {
      q: "What is 2 + 2?",
      answers: [
        {
          text: "4",
          is_correct: true,
        },
        {
          text: "3",
          is_correct: false,
        },
        {
          text: "Fish",
          is_correct: false,
        },
        {
          text: "5",
          is_correct: false,
        },
      ],
    },
    {
      q: 'How many letters are in the word "Banana"?',
      answers: [
        {
          text: "5",
          is_correct: false,
        },
        {
          text: "7",
          is_correct: false,
        },
        {
          text: "6",
          is_correct: true,
        },
        {
          text: "12",
          is_correct: false,
        },
      ],
    },
    {
      q: "Find the missing letter: C_ke",
      answers: [
        {
          text: "e",
          is_correct: false,
        },
        {
          text: "a",
          is_correct: true,
        },
        {
          text: "i",
          is_correct: false,
        },
      ],
    },
  ],
  results: [
    {
      min: 0,
      max: 2,
      title: "Try again!",
      desc: "Do a little more studying and you may succeed!",
    },
    {
      min: 3,
      max: 3,
      title: "Wow, you're a genius!",
      desc: "Studying has definitely paid off for you!",
    },
  ],
});
const questionsAnswered = ref(0);
const totalCorrect = ref(0);
const questionAnswered = (is_correct) => {
  if (is_correct) {
    totalCorrect.value++;
  }
  questionsAnswered.value++;
};
const reset = () => {
  totalCorrect.value = 0;
  questionsAnswered.value = 0;
};
</script>

<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < data.questions.length"
        :questions="data.questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
        :totalCorrect="totalCorrect"
      />
      <result v-else :results="data.results" :totalCorrect="totalCorrect" />
    </transition>
    <transition-group name="delay">
      <button
        type="button"
        class="reset-btn"
        @click.prevent="reset"
        v-if="questionsAnswered === data.questions.length"
      >
        Reset
      </button>
    </transition-group>
  </div>
</template>

<style></style>
