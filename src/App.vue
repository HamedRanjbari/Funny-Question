<template>
  <div id="app">
    <hamed-header :correctCount="correctCount" :totalCount="totalCount" />

    <b-container class="bv-example-row my-5">
      <b-row>
        <b-col sm="8" offset="2" mt="5">
          <hamed-content
            v-if="questionList.length"
            :next="next"
            :cQuestion="questionList[index]"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import hamedHeader from "./components/hamed-header.vue";
import hamedContent from "./components/hamed-content.vue";

export default {
  name: "App",
  components: {
    hamedHeader,
    hamedContent,
  },
  data() {
    return {
      questionList: [],
      index: 0,
      correctCount: 0,
      totalCount: 0,
    };
  },
  methods: {
    next() {
      if (this.index < 9) {
        this.index++;
      }
    },
    increment(is_Correct) {
      if (is_Correct) {
        this.correctCount++;
      }
      this.totalCount++;
    },
  },
  mounted() {
    fetch(
      "https://opentdb.com/api.php?amount=9&category=18&difficulty=hard&type=multiple",
      {
        method: "get",
      }
    )
      .then((Response) => {
        return Response.json();
      })
      .then((result) => {
        this.questionList = result.results;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
