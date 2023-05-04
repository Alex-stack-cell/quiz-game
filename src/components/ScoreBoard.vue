<template>
    <section class="score"> 
        Player
        <span>{{ userScore }}</span> x <span>{{ computerScore }}</span>
        Computer
    </section>
</template>

<script>
export default {
    name: 'ScoreBoard',
    props: [
        'userScore',
        'computerScore'
    ]
  
}
</script>

<style lang="scss">
section.score {
    display: block;
    border-bottom: 1px solid #000;
    padding: 24px;
    font-size: 10px;
    span {
       padding: 8px;
       font-weight: bold;
       border: 1px solid #000; 
    }
}
</style>