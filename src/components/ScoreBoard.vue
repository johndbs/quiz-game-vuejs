<template>
    <section class="score">
        Player <span>0</span>  x <span>0</span> Computer
    </section>
</template>

<script lang="ts">

import { Options, Vue } from 'vue-class-component';
@Options({
    components: {
        
    },
})
export default class ScoreBoard extends Vue {
    score = 0;
    correctAnswers = 0;
    incorrectAnswers = 0;
    questions = 0;
    getScore(){
        this.score = (this.correctAnswers / this.questions) * 100;
    }
}

</script>

<style lang="scss">
.score {
    display: flex;
    justify-content: space-between;
    font-size: 1.5rem;
    padding: 1rem;
    background-color: #f5f5f5;
    border-radius: 0.5rem;
    margin: 1rem 0;
}
</style>