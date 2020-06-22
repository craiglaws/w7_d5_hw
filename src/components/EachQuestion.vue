<template lang="html">
  <div>
    <p v-html="question.question"></p>
    <!-- <label v-for="(answer, index) in sortAnswers" :id="index" :key="index">{{answer.answer}}</label> -->

    <div v-for="(answer, index) in sortAnswers" :key="index" :class="changeClass" >
        <!-- picked(not null) (answer.value ? greenClass : redClass )  : normalClass -->

      <label  :for="answer.answer">{{answer.answer}} </label>
      <input type="radio" :value="answer" v-model="picked" :name="question.question" :id="answer.answer">

    </div>
      <!-- <input type="radio" :id="index" :value="answer" > -->
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
      console.log(answer.target.value);
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
    },

    changeClass(){
      let className = 'default';
      if (this.picked == null){
        return className
      }

      if (this.picked.value){className = 'correct';}
      else if (this.picked.value == false){className = 'wrong'}

      return className;
    }

  }
}
</script>

<style lang="css" scoped>
.correct{
  background-color: green;
}

.wrong{
  background-color: red;
}

.default{

}

</style>
