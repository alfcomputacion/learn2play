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
            <input autofocus ref="inputsx" v-model="input" type="text" placeholder="Type here">
      
            </div>  
    {{input}}
              <div v-if="guessedArray.length > 0">
                    <ol>
                        <li class="text-center" v-for="item in guessedArray" :key="item">{{item}}</li>
                    </ol>
                </div>
        </div>
        </template>
        </transition>
        <transition>
          <template>
            <div>
              <!--! Points  -->
              <div  id="game-points" class="gameon">2 <strong>++</strong></div>
              <!-- ! Time -->
              <div  id="game-time-animation" class="gameon">0</div>
            </div>
          </template>
        </transition>
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
      maxNumber: '5',
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
        currentAnagram: [],
        guessedArray: [],
        anagramsLeft: 0,
        miCampo: null,
        inputFocus: false

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
  mounted() {
    
    console.log(this.inputFocus)
  },
  methods:{
    showInput() {
      this.inputFocus = true
      setTimeout(() => {
        let elem = document.getElementById('myInput')
        let clickEvent = new Event('click')
        elem.dispatchEvent(clickEvent)
        elem.focus()
        console.log('el elemento ' +elem.value)

      }, 2000);
      
      // Show the input component
      // this.inputIsVisible = true;

      // Focus the component, but we have to wait
      // so that it will be showing first.
      // this.nextTick(() => {
      //   this.inputFocus = true
      //   // this.focusInput();
      // });
    },
    focusInput() {
      this.$refs.inputsx.focus();
    },
    config(){
        this.screen= 'config'

    },

    play(){
          this.screen = 'play';
          this.startTimer();
          this.newAnagram();
                  
    },
      restart(){
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
            this.guessedArray.push(value)
            this.currentArray = this.currentArray.filter(item => item !== value)
            this.anagramsLeft = this.currentArray.length
            this.input = ''
            this.score++
             if(this.currentArray.length === 0){
                     this.guessedArray = []
                     setTimeout(this.newAnagram, 300);
                }
            return
         }

      },
        checkAnswer(value){
          return this.input.toLowerCase() === value;

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
            this.guessedArray = []
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
      }else if (e.keyCode === 8){
        this.input = this.input.substring(0, this.input.length-1);
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
#game-points, #game-time-animation,#question-mark{
    display: none;
}

/*#endregion Game  */


/*todo ANIMATION  */
/*#region ANIMATION  */
#game-points{
    position: absolute;
    display: flex;
    top: 40%;
    left: 75%;
    color: var(--brigth-y);
    z-index: -1000;

}
#game-time-animation{
position: absolute;
display: flex;
top: 50%;
left: 75%;
color: var(--brigth-r);
z-index: -1000;

}
.animate-seconds{
    animation: scaledown 2s ease;
}
.animate-minimize{
    animation: scaledown 2s ease;
}
@keyframes scaledown {
    0%{
        z-index: 1000;
        transform: scale(8);
        opacity: 1;
    }
  
    100%{
        z-index: 1;
        transform: scale(1);
        opacity: 0;
    }
}
/* } */
/*#endregion ANIMATION  */

</style>