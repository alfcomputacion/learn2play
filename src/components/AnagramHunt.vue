<template>
    <div class="main-container">
        <div v-for="anagram in anagrams" :key="anagram"  class="header-space">
            <p>{{anagram[maxNumber] }}</p>
        </div>
        <div v-if="screen === 'config'" id="config-container">
        <h1>Anagram Hunt</h1>
        <SelectInput 
            :currentValue="maxNumber"
            v-model="maxNumber"
            label="Word length"
            id="wordLength"
            :options="numbers"/>
        <ol>
            <li>Chose Word Length</li>
            <li>Press <strong>Play!</strong></li>
            <li>How many anagrams can you find in a minute?</li>
        </ol>
        <PlayButton 
            :btnclass="btnClass"
            :label="btnLabel"
            @le-button-click="play"
            />
        </div>
        <div v-else-if="screen === 'play'" id="game-container">
             <div class="row border-bottom" id="scoreboard">
            <div class="col px-3 text-left">
                <Score />
            </div>
            <div class="col px-3 text-right">
                <Timer />
            </div>
        </div>
        <!-- <div  class="row text-secondary my-2" id="equation">
              <p><strong>Word goes here and also (word qty)</strong></p>
              <Equation :question="question"
                :answer="input"
                :answered="answered" />

        </div>   -->
        <input type="text" placeholder="Type here">

        </div>

    </div>
</template>

<script>
import SelectInput from './SelectInput.vue'
import PlayButton from './PlayButton.vue';
import Score from './Score.vue';
import Timer from './Timer.vue';
import Equation from './Equation.vue';
import {randInt, anagrams} from '../helpers/helpers'
// import anagrams from '../../public/anagrams.json'

export default {
  name: 'AnagramHunt',
  data: function(){
    return{
      maxNumber: '5',
    //   wordLength: [5,6,7,8],
      screen: 'config',
      input: '',
      operands: {num1: '1', num2: '1'},
        answered: false,
        score: 0,
        gameLength: 60,
        timeLeft: 0,
        btnLabel: 'Play!',
        btnClass: 'btn form-control btn-primary',
        anagrams

    }

  },
  computed: {
    numbers: function(){
         const numbers = [];
         for(let number=5; number <= 8; number++){
          numbers.push([number,number]);
         }
         return numbers;
    },
    
    // question: function(){
    //     const num1 = this.operands.num1;
    //     console.log(this.operands.num1);
    //     const num2 = this.operands.num2;
    //     const equation = `${num1} ${this.operation} ${num2}`;
    //     return equation;
    // }
 
  },
  methods:{
    config(){
        this.screen= 'config'
    },

    play(){
          this.screen = 'play';
          this.newQuestion();
    },
    clearAnswer(){
        this.input = ''
    },
    setInput(value) {
        this.input += String(value);
        this.input = String(Number(this.input));
        this.answered = this.checkAnswer(this.input, 
                                        this.operation,
                                        this.operands);
        if (this.answered) {
          setTimeout(this.newQuestion, 300);
          this.score++;
        }
      },
    getRandomNumbers(operator, low, high){
        let num1 = randInt(low, high);
        let num2 = randInt(low, high);
        const numHigh = Math.max(num1, num2);
        const numLow = Math.min(num1, num2);

        if(operator === '-'){
            num1 = numHigh;
            num2 = numLow;
        }

        if(operator === '/'){
            if(num2 === 0){
                num2 = randInt(1, high);
            }
            num1 = (num1 * num2);
        }
        return {num1, num2};
    },

    newQuestion(){
        const arraySize = this.anagrams[this.maxNumber]//arrays in the array
        const firstInside = this.anagrams[this.maxNumber][0] 
        const wordLength = this.anagrams[this.maxNumber][0][0] //SIZE OF THE word

    const five = this.anagrams[this.maxNumber][randInt(0, 2)][randInt(0, 3)]
    const six = this.anagrams[this.maxNumber][2][randInt(0, firstInside-1)]

    console.log('Arrays qty: ' + this.anagrams[this.maxNumber])
    console.log('Arrays qty: ' + arraySize)
    console.log('Anagrams in array: ' +this.anagrams[this.maxNumber][0])
    console.log('Anagrams in array: ' + firstInside)
    console.log('word Length: ' +this.anagrams[this.maxNumber][0][0])
    console.log('Word Length: ' + wordLength)
    
    
    console.log(six)


        // this.input = '';
        // this.answered = false;
        // this.operands = this.getRandomNumbers(
        //     this.operation, 0 , this.maxNumber);
    },
    checkAnswer(userAnswer, operation, operands){
        if(isNaN(userAnswer)) return false;

        let correctAnswer;
        switch(operation){
            case '+':
            correctAnswer = operands.num1 + operands.num2;
            break
            case '-':
            correctAnswer = operands.num1 - operands.num2;
            break
            case 'x':
            correctAnswer = operands.num1 * operands.num2;
            break
            default : //division
            correctAnswer = operands.num1 / operands.num2;
            break
        }
        return (parseInt(userAnswer) === correctAnswer);
    }
  },
// created(){
//     const five = this.anagrams[this.maxNumber][this.maxNumber.length][0]
//     const six = this.anagrams[7][0][2]
//     console.log(five)
//     console.log(six)

    
// },  
  components: {
    SelectInput,
    PlayButton,
    Score,
    Timer,
    Equation
}
}
</script>

<style scoped>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;

} */
.header-space{
  margin-top: 4rem;
}

.main-container{
    margin: auto;
    width: 380px;
}

button.number-button{
    border-radius: .25em;
    font-size: 3em;
    height: 2em;
    margin: .1em;
    text-align: center;
    width: 2em;
}
#clear-button{
    border-radius: .25em;
    font-size: 3em;
    margin: .1em;
    text-align: center;
    width: 4.2em;
}
#scoreboard{
    font-size: 1.5em;
}
</style>