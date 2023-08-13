<template>
  <div>
    <div>
      <b-jumbotron>
        <template>{{ cQuestion.question }}</template>

        <hr class="my-4" />

        <b-list-group>
          <b-list-group-item
            class="changeHover"
            v-for="(answer, i) in shuffledAnswers"
            :key="i"
            @click="changeIdx(i)"
            :class="[
              !answered && cIndex === i
                ? 'selected'
                : answered && i === correctAnswer
                ? 'correct'
                : answered && i !== correctAnswer
                ? 'wrong'
                : '',
            ]"
          >
            {{ answer }}
          </b-list-group-item>
        </b-list-group>

        <b-button
          class="m-2"
          @click="submitAnswer()"
          :disabled="cIndex === null || answered"
          variant="primary"
          href="#"
          >Submit</b-button
        >
        <b-button class="m-2" @click="next()" variant="success" href="#"
          >Next</b-button
        >
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    cQuestion: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      cIndex: null,
      shuffledAnswers: [],
      correctAnswer: null,
      answered: false,
    };
  },
  watch: {
    cQuestion: {
      immediate: true,
      handler() {
        (this.cIndex = null),
          (this.answered = null),
          (this.correctAnswer = null),
          this.randomize();
      },
    },
  },
  methods: {
    changeIdx(i) {
      this.cIndex = i;
    },
    randomize() {
      let allAnswer = [
        ...this.cQuestion.incorrect_answers,
        this.cQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(allAnswer);
      this.correctAnswer = this.shuffledAnswers.indexOf(
        this.cQuestion.correct_answer
      );
    },
    submitAnswer() {
      let is_Correct = false;
      if (this.cIndex === this.correctAnswer) {
        is_Correct = true;
      }
      this.answered = true;
      this.increment(is_Correct);
    },
  },
  computed: {
    answers() {
      let answers = [...this.cQuestion.incorrect_answers];
      answers.push(this.cQuestion.correct_answer);
      return answers;
    },
  },
};
</script>

<style scoped>
.changeHover {
  transition: 800ms;
}
.changeHover:hover {
  background-color: #dedede;
  cursor: pointer;
}
.selected {
  background-color: rgb(62, 181, 255);
}
.correct {
  background-color: lightseagreen;
}
.wrong {
  background-color: rgb(255, 94, 94);
}
</style>
