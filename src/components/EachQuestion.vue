<template lang="html">
  <div>
    <p>{{question.question}}</p>
    <!-- <label v-for="(answer, index) in sortAnswers" :id="index" :key="index">{{answer.answer}}</label> -->
    <div>
      <label  v-for="(answer, index) in sortAnswers" :key="index" :for="index">{{answer.answer}} <input type="radio" :value="answer" v-model="picked" :name="question.question" :id="index" >  </label>
      <!-- <input type="radio" :id="index" :value="answer" > -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'each-question',
  props: ['question'],
  data(){
    return {
      correctAnswer: null,
      picked: null
    }
  },
  methods: {
    shuffleAnswers(array){
      array.sort(() => Math.random() - 0.5)
    },
    checkAnswer(answer){
      console.log(answer);
    },
    selectRightAnswer(rightAnswer){
      this.correctAnswer = rightAnswer
    }
  },

  computed: {
    sortAnswers(){
      const answerArray = this.question.incorrect_answers.map(eachAnswer => {
        const wrongAnswer = {}
        wrongAnswer.value = false
        wrongAnswer.answer = eachAnswer
        return wrongAnswer
      })
      const rightAnswer = {}
      rightAnswer.value = true
      rightAnswer.answer = this.question.correct_answer
      this.selectRightAnswer(rightAnswer);
      answerArray.push(rightAnswer);
      this.shuffleAnswers(answerArray)
      return answerArray;
    }

  }
}
</script>

<style lang="css" scoped>
</style>
