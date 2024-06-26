<template>
  <div v-if="this.question">
    <h1 v-html="this.question"></h1>

    <template v-for="(answer, index) in answers" :key="index">
      <input type="radio" name="options" value="answer">
      <label v-html="answer"></label><br>
    </template>

    <button class="send" type="button"> Send</button>

  </div>


</template>

<script lang="ts">
import { computed } from 'vue';
import { Options, Vue } from 'vue-class-component';

@Options({
  components: {

  },
})
export default class App extends Vue {
  question = ''; 
  incorrectAnswers: string[] = [];
  correctAnswer = '';

  answers = computed(()=>{
      let answers: string[] = JSON.parse(JSON.stringify(this.incorrectAnswers)); 
      answers.splice(Math.round(Math.random() * this.correctAnswer.length), 
        0, 
        this.correctAnswer);
      return answers;
  });


  created(): void {
      this.axios.get("https://opentdb.com/api.php?amount=1&difficulty=easy").then((response) => {
        console.log(response.data);
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0].incorrect_answers;
        this.correctAnswer = response.data.results[0].correct_answer;
      }).catch((error)=>{
        console.error(error);
      });
  }



}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type=radio]{
    margin: 12px 4px;
  }

  button-send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 160px;
    color: #ffff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }


}
</style>
