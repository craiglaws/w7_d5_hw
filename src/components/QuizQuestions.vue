<template lang="html">
  <div>
    <each-question v-for="(question, index) in questions" :key="index" :question="question"> </each-question>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import EachQuestion from './EachQuestion.vue'
export default {
  name: 'quiz-questions',
  data(){
    return {
      questions: null
    }
  },
  mounted(){
    eventBus.$on('start-quiz', (id) => this.getQuestions(id))
  },
  methods: {
    getQuestions(id){
      fetch(`https://opentdb.com/api.php?amount=10&type=multiple&category=${id}`)
        .then(result => result.json())
        .then(data => this.questions = data.results)
    }
  },
  components: {
    "each-question": EachQuestion
  }
}
</script>

<style lang="css" scoped>
</style>
