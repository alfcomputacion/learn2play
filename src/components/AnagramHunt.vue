<template>
<div class="main-container">
  <div class="header-space"></div>
  <!--#region config  -->
  <div v-if="screen === 'config'" id="config-container">
        <h1>Anagram Hunt</h1>
        <SelectInput 
            :currentValue="maxNumber"
            v-model="maxNumber"
            label="Word length"
            id="theWord"
            :options="numbers"/>
        <ol>
            <li>Choose Word Length</li>
            <li>Press <strong>Play!</strong></li>
            <li>How many anagrams can you find in a minute?</li>
        </ol>
        <PlayButton 
            :btnclass="btnClass"
            :label="btnLabel"
            @le-button-click="play"
            />
  </div>
  <!-- #endregion config -->
 <!-- #region div play -->
  <div v-else-if="screen === 'play'" id="game-container">
      <transition name="slide">
      <template v-if="timeLeft === 0">
          <div class="text-center">
              <h2>Time's Up!</h2>
              <strong class="big">You Answered</strong>
              <div class="huge">{{score}}</div>
              <strong class="big">Anagrams Correctly</strong>
              <div class="big" v-if="arrayFromAnagrams.length === 0">Congratulations you guessed all "ANAGRAMS" with {{maxNumber}} letters</div>
              <button class="btn btn-primary form-control m-1"  
              @click="restart()">
              Play Again with Same Settings
              </button>
              <button class="btn btn-secondary form-control m-1"
              @click="config()">
              Change Settings
              </button>
          </div>
      </template>
      </transition>

      <transition name="slide-right">
      <template v-if="timeLeft > 0">
          <div>
            <div class="row border-bottom" id="scoreboard">
              <div class="col px-3 text-left">
                <Score :score="score" />
              </div>
              <div class="col px-3 text-right">
                <Timer :timeLeft="timeLeft"/>
              </div>
            </div>
            <div v-for="anagram in anagrams" :key="anagram"  >
                <!-- <p>{{anagram[maxNumber] }}</p> -->

            </div>
                <div class="text-center" v-if="currentAnagram.length > 0">
                <!-- <h3>{{currentArray}} {{ currentArray.length}}</h3> -->
           
                    <h2><strong>{{currentAnagram}} </strong> (<span class="anagrams">{{anagramsLeft}}</span> left)</h2>
                </div>
          
            <div class="text-center">
            <input autofocus v-model="input" type="text" placeholder="Type here">

            </div>  
    <!-- {{input}} -->
     
              <div v-if="guessedArray.length > 0">
                    <ol>
                        <li class="text-center bigger" v-for="item in guessedArray" :key="item">{{item}}</li>
                    </ol>
                </div>
        </div>
        </template>
        </transition>
        <div  id="game-points" class="gameon">1 <strong>++</strong></div>
 
  </div>
<!-- #endregion div play -->
</div><!-- end div container -->
</template>

<script>
import SelectInput from './SelectInput.vue'
import PlayButton from './PlayButton.vue';
import Score from './Score.vue';
import Timer from './Timer.vue';
import Equation from './Equation.vue';
import {randInt, anagrams} from '../helpers/helpers'

export default {
  name: 'AnagramHunt',
  data: function(){
    return{
      maxNumber: '8',
    //   theWord: [5,6,7,8],
      screen: 'config',
      input: '',
        answered: false,
        score: 0,
        gameLength: 60,
        timeLeft: 0,
        btnLabel: 'Play!',
        btnClass: 'btn form-control btn-primary',
        anagrams,
        currentArray: '',
        wordLenghtArrays:[],
        currentAnagram: [],
        guessedArray: [],
        anagramsLeft: 0,
        arrayFromAnagrams: [],
        miCampo: null,
        inputFocus: false,
        gameOver: false
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

  },
  unmounted(){clearInterval(this.timer);},
  methods:{
    animatePoints(){
        const score = document.getElementById('game-points');
            score.className += ' animate-minimize';
                console.log('answer empty ')
                setTimeout(() => {
                    console.log('time is 400');
                    score.classList.remove('animate-minimize')
                }, 400);
    },

    config(){
        this.screen= 'config'

    },

    play(){
      this.arrayFromAnagrams = anagrams[this.maxNumber].slice(0)

        this.gameOver = false
          this.screen = 'play';
          this.startTimer();
          this.newAnagram();
// if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) {
//  alert(navigator.userAgent)
// }        
                  
    },
      restart(){
      this.arrayFromAnagrams = anagrams[this.maxNumber].slice(0)
      this.gameOver = false
      this.score = 0;
      this.startTimer();
      this.newAnagram();
      this.input = ''
    },
    clearAnswer(){
        this.input = ''
    },
    setInput(value) {
       
         if(this.currentArray.find(this.checkAnswer)){
          this.animatePoints()
            this.guessedArray.push(value)
            this.currentArray = this.currentArray.filter(item => item !== value)
            this.anagramsLeft = this.currentArray.length
            this.input = ''
            this.score++
             if(this.currentArray.length === 0){
                     this.guessedArray = []
                     if(this.wordLenghtArrays.length > 0){
                        setTimeout(this.newAnagram, 300);
                     }else{
                        this.timeLeft = 1
                     }
                     
                }
            return
         }

      },
        checkAnswer(value){
          return this.input.toLowerCase() === value;

        },

    newAnagram(){
        this.wordLenghtArrays = this.arrayFromAnagrams

        let index = randInt(0, this.wordLenghtArrays.length-1)
 
                const firstInside = this.wordLenghtArrays[index]  //Current array with selected size (5,6,7 or 8)
              
                let index2 = randInt(0, firstInside.length-1)
                const theWord = this.wordLenghtArrays[index][index2] //THE word to play anagram from
              
                this.currentArray = firstInside
        
            this.currentArray = firstInside.filter(item => item !== theWord)
            this.anagramsLeft = this.currentArray.length
            
            // console.log(this.currentAnagram)
            // console.log('this is the current array-* ' +  this.guessedArray)
            this.currentAnagram = theWord
            // console.log(theWord)

                if(this.wordLenghtArrays.length > 0){
                    this.wordLenghtArrays.splice(index,1) //remove array that is been plyaing
                }

       
    },
startTimer(){
      window.addEventListener('keyup', this.handleKeyUP);
      // console.log(this.timeLeft);
      this.timeLeft = this.gameLength;
      // console.log(this.timeLeft);
      if(this.timeLeft > 0){
        this.timer = setInterval(() =>{
          this.timeLeft--;
          // console.log(this.timeLeft);
          if(this.timeLeft === 0){
            clearInterval(this.timer);
            this.guessedArray = []
            this.wordLenghtArrays = []
             window.removeEventListener('keyup', this.handleKeyUP)
          }
        }, 1000)
      }

    },
    // todo it needs fix
handleKeyUP(e){
      e.preventDefault();
      if(e.keyCode === 32 || e.keyCode === 13 ){
        this.setInput(this.input.toLowerCase())
        this.clearAnswer();
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
.header-space{
  margin-top: 4rem;
}

.main-container{
    margin: auto;
    width: 380px;
}




</style>