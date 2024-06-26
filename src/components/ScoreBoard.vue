<template>
    <section class="score">
        Player <span>{{winCount }}</span>  x <span>{{ loseCount }}</span> Computer
    </section>
</template>

<script lang="ts">

import { Options, Vue } from 'vue-class-component';
import { Prop } from 'vue-property-decorator';

@Options({
    components: {
        
    },
})
export default class ScoreBoard extends Vue {

    @Prop({type: Number, required: true}) winCount!: number;
    @Prop({type: Number, required: true}) loseCount!: number;
    
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