<template>
    <strong>Time Left: <span class="timer-seconds">{{timeLeft}}</span></strong>
</template>

<script>
    export default{
        name: 'Timer',
        props: {
            timeLeft: Number
        }
    }
</script>

<style scoped>
.timer-seconds{
    text-shadow: 0 0  .1rem black;
    animation: seconds 60s ease;
}
@keyframes seconds {
    0%{
    
        color: green;
        font-size: 1.5rem;
    }
    50%{
     
        color: orange;
        font-size: 1.6rem;
    }
    100%{
        font-size: 1.7rem;
        color: red;
    }
}
</style>