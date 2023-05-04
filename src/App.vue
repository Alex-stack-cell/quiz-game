<template>
  <div>
    <template v-if="this.question">
      <h1 v-html="this.question">
      </h1>
    
      <template v-for="(answer, index) in this.answers" v-bind:key="index">
          <input
            :disabled="this.answerSubmitted" 
            type="radio"
            name="options"
            :value="answer"
            :id="index + 1"
            v-model="this.chosenAnswer"
            >
          
          <label v-html="answer" :for="index + 1"></label><br>
      </template>
      <button @click="this.submitAnswer()" class="send" type="button">Send</button>
      <section 
        class="result"
        v-if="this.answerSubmitted"
      >
        <h4 
          v-if="this.chosenAnswer!=this.correctAnswer"
        > &#10060;You picked the wrong answer. The correct answer is {{ this.correctAnswer }}</h4>
        <h4
          v-else
        >
          &#9989; Congratulations, the answer is : {{ this.correctAnswer }} is correct.
        </h4>
      </section>
    </template>

  
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
      chosenAnswer: undefined,
      answerSubmitted: false
    }
  },
  computed: {
    answers() {
      // this trick prevents from modifying this.incorrectAnswers when new data are pushed in answers array
      // because there is data are binded between answers and this.incorrectAnswers
      const answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      const randomPosition = Math.round((Math.random() * answers.length));
      
      answers.splice(randomPosition, 0, this.correctAnswer);

      return answers;
    }
  },
  methods: {
    submitAnswer: function () {
      if (!this.chosenAnswer) {
        alert('Please pick one of the options');

        return;
      } else {
        this.answerSubmitted = true;
      }

      if (this.chosenAnswer == this.correctAnswer) {
        console.log('Correct ! :D');
      } else {
        console.log('Wrong ! :( )')
      }
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
