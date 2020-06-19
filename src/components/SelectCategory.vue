<template lang="html">
  <div>
    <select v-model="selectedCategory">
      <!-- <option disabled value="">Please select a category</option> -->
      <option v-for="(category, index) in categories" :key="index" :value="category">{{category.name}}</option>
    </select>
    <button v-on:click="handleStartQuiz">Start Quiz</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'select-category',
  data(){
    return{
      categories: null,
      selectedCategory: null
    }
  },
  mounted(){
    fetch('https://opentdb.com/api_category.php')
    .then(result => result.json())
    .then(data => this.categories = data.trivia_categories)
  },
  methods: {
    handleStartQuiz(){
      eventBus.$emit('start-quiz', this.selectedCategory.id)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
