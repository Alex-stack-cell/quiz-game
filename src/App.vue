<template>
  <div>
    <h1 v-html="this.question">
    </h1>
    
    <input type="radio" id="trueOption" name="options" value="true">
    <label for="trueOption">True</label><br>
    
    <input type="radio" id="falseOption" name="options" value="false">
    <label for="falseOption">False</label><br>

    <button class="send" type="button">Send</button>

  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
    }
  },
  computed: {
    answers() {
      // this trick prevents from modifying this.incorrectAnswers when new data are pushed in answers array
      // because there is data are binded between answers and this.incorrectAnswers
      const answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      const randomPosition = Math.round((Math.random() * answers.length));
      
      return answers.splice(randomPosition, 0, this.correctAnswer);
    }
  },
  created() {
    const api = 'https://opentdb.com/api.php?amount=1&category=18&difficulty=easy';

      this.axios
        .get(api)
        .then((response) => {
          this.question = response.data.results[0].question;
          this.incorrectAnswers = response.data.results[0].incorrect_answers;
          this.correctAnswer = response.data.results[0].correct_answer;
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

  input[type=radio] {
  margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }
}
</style>
