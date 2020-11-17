<template>
  <div>
    <b-jumbotron>
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, i) in answers"
          :key="i"
          @click="selectAnswer(i)"
          :class="[selectedIndex === i ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox",
  props: { currentQuestion: Object, next: Function },
  data() {
    return {
      selectedIndex: null,
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
  methods: {
    selectAnswer(i) {
      this.selectedIndex = i;
    },
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
  cursor: pointer;
}
.list-group-item:hover {
  background: #eee;
}
.btn {
  margin: 0 5px;
}

.selected {
  background: lightblue;
}
.correct {
  background: lightgreen;
}
.incorrect {
  background: red;
}
</style>
