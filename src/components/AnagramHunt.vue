<template>
    <div class="main-container">
        <div class="header-space"></div>
          
            
        <div v-if="screen === 'config'" id="config-container">
        <h1>Anagram Hunt</h1>
        <SelectInput 
            :currentValue="maxNumber"
            v-model="maxNumber"
            label="Word length"
            id="theWord"
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
                <Score :score="score" />
            </div>
            <div class="col px-3 text-right">
                <Timer :timeLeft="timeLeft"/>
            </div>
        </div>
        <div v-for="anagram in anagrams" :key="anagram"  >
            <p>{{anagram[maxNumber] }}</p>

        </div>
            <div class="text-center" v-if="currentAnagram.length > 0">
            <h3>{{currentArray}} {{ currentArray.length}}</h3>
                <h2><strong>{{currentAnagram}} </strong> ({{anagramsLeft}} left)</h2>
            </div>
        <!-- <div  class="row text-secondary my-2" id="equation">
              <p><strong>Word goes here and also (word qty)</strong></p>
              <Equation :question="currentAnagram"
                :answer="input"
                :answered="answered"
                :anagram="true" />

        </div>   -->
        <div class="text-center">
        <input disabled v-model="input" type="text" placeholder="Type here">
        </div>  
{{input}}
        </div>
          <div v-if="guessedArray.length > 0">
                <ol>
                    <li class="text-center" v-for="item in guessedArray" :key="item">{{item}}</li>
                </ol>
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
    //   theWord: [5,6,7,8],
      screen: 'config',
      input: '',
      operands: {num1: '1', num2: '1'},
        answered: false,
        score: 0,
        gameLength: 60,
        timeLeft: 0,
        btnLabel: 'Play!',
        btnClass: 'btn form-control btn-primary',
        anagrams,
        currentArray: '',
        currentAnagram: [],
        guessedArray: [],
        anagramsLeft: 0

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
          this.startTimer();
          this.newAnagram();
    },
    clearAnswer(){
        this.input = ''
    },

    // todo it needs fix
    setInput(value) {
         this.input += String(value);
         if(this.currentArray.find(this.checkAnswer)){
            this.guessedArray.push(this.input)
            this.currentArray = this.currentArray.filter(item => item !== this.input)
            this.input = ''
            this.score++
             if(this.currentArray.length === 0){
                     setTimeout(this.newAnagram, 300);
                }
            return
         }

      },
      // todo it needs fix
        checkAnswer(value){
            if(this.input === value){
                return true
            }else{
                return false
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

    newAnagram(){
        
        const arraySize = this.anagrams[this.maxNumber]//arrays in the array
        let index = randInt(0, arraySize.length-1)
        const firstInside = this.anagrams[this.maxNumber][index]  //Current array with selected size (5,6,7 or 8)
        let index2 = randInt(0, firstInside.length-1)
        const theWord = this.anagrams[this.maxNumber][index][index2] //THE word to play anagram from
   
   this.currentArray = firstInside
  
    // this.guessedArray = firstInside.filter(item => item !== theWord)
    this.currentArray = firstInside.filter(item => item !== theWord)
    this.anagramsLeft = this.currentArray.length
    
    console.log(this.currentAnagram)
    console.log('this is the current array-* ' +  this.guessedArray)

  
    this.currentAnagram = theWord
   console.log(theWord)

 
    },
      startTimer(){
      window.addEventListener('keyup', this.handleKeyUP);
      console.log(this.timeLeft);
      this.timeLeft = this.gameLength;
      console.log(this.timeLeft);
      if(this.timeLeft > 0){
        this.timer = setInterval(() =>{
          this.timeLeft--;
          console.log(this.timeLeft);
          if(this.timeLeft === 0){
            clearInterval(this.timer);
             window.removeEventListener('keyup', this.handleKeyUP)
          }
        }, 1000)
      }

    },
    // todo it needs fix
       handleKeyUP(e){
      e.preventDefault();
    
      if(e.keyCode === 32 || e.keyCode === 13 ){
        this.clearAnswer();
      }else if (e.keyCode === 8){
        this.input = this.input.substring(0, this.input.length-1);
      }else{
        this.setInput(e.key);
      }
    }
  },

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