<template>
  <div>
    <h1>
      Microphones can be used not only to pick up sound, but also to project sound similar to speaker.
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

  created() {
    const api = 'https://opentdb.com/api.php?amount=1&category=18&difficulty=easy';

      this.axios
        .get(api)
        .then((response) => {
          console.log(response.data.results[0])
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
