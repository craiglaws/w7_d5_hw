<template lang="html">
  <div>
    <h1>QUIZ</h1>
    <select-category> </select-category>
    <quiz-questions> </quiz-questions>
  </div>
</template>

<script>
import SelectCategory from './components/SelectCategory.vue'
import QuizQuestions from './components/QuizQuestions.vue'
export default {
  name: 'app',
  data(){
    return {
      questions: []
    }
  },
  components: {
    "select-category": SelectCategory,
    "quiz-questions": QuizQuestions
  }
  // mounted(){
  //   fetch('https://opentdb.com/api.php?amount=10&type=multiple')
  //   .then(result => result.json())
  //   .then(data => this.questions = data)
  // }

}
</script>



<style lang="css" scoped>
</style>
