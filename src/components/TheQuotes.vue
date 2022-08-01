<template>
    <div class="container">
    <div class="header-space"></div>   
    <div class="quotes">
         <h2 class="text-center">{{searchQuote.title}}</h2>
            <p>{{searchQuote.quote}}</p>
            <div v-if="searchQuote.quote === 'loading...'" class="spinner"></div>
            <p class="text-right"><em>{{searchQuote.author}}</em></p>
        </div> 
           
        <div class="games row">
            <div class="mathificent col-lg-6">
                 <h4>       
                            Anagram Hunt
                        </h4>
                        <div>
                            An anagram is a word or phrase formed by rearranging the letters of a 
                            different word or phrase, typically using all the original letters 
                            exactly once.[1] For example, the word anagram itself can be rearranged 
                            into nag a ram, also the word binary into brainy and the word adobe into abode.
                        </div>
                <PlayButton 
                    :btnclass="btnClass"
                    :label="btnLabel"
                    @le-button-click="$emit('goto-page', 'anagram')"
                />
            </div>
            <div class="anagram col-lg-6">
                  <h4>       
                     Math Fact Practice
                </h4>
                    <div>
                        This is a simple game to test your skills in math Addition, Subtraction, Multiplication and Division.
                        THe game will run for 30 seconds and you will have to answer as many questions as you posible can.
                        Be careful it is addictive.
                        We are not responsible if you can't stop Playing.
                        So Have fun!!!
                    </div>
                <PlayButton 
                    :btnclass="btnClass"
                    :label="btnLabel"
                    @le-button-click="$emit('goto-page', 'mathificent')"
                    />
            </div>
        </div>
    </div>
</template>

<script>

import quotesData from '../../public/quotes.json'
import { randInt } from '@/helpers/helpers';
import PlayButton from './PlayButton.vue';

    export default{
    name: "TheQuotes",
    data: function () {
        return {
            quotes: quotesData,
            searchQuote: {
                title: "loading...", 
                quote: "loading...", 
                author: "loading..."},
            quoteId: 1,
            quotesInterval: null,
            show: true,
            btnClass: "btn btn-primary form-control",
            btnLabel: 'Play!'
        };
    },
    computed: {},
    methods: {
        randomQuote() {
            // check if already an interval has been set up
            //! try
            //todo
            //**** */
            this.quotesInterval = setInterval(() => {
            let tmp = this.quoteId
              this.quoteId =  randInt(1, 7)
              console.log('disque random# ' + this.quoteId)
              if(tmp === this.quoteId){
                this.quoteId =  randInt(1, 5)
              }
           
                this.show = !this.show;
                console.log(this.searchQuote);
                this.searchQuote = this.quotes[this.quoteId];
                console.log("From quotes " + this.quoteId);
                return this.searchQuote;
            }, 10000);
        },
    },
    mounted() {
        this.searchQuote = this.quotes[1];
        this.randomQuote();
        console.log("created...");
    },
    unmounted() {
        clearInterval(this.quotesInterval);
    },
    components: { PlayButton }
}
</script>

<style scoped>
.header-space{
  margin-top: 4rem;
}
.quotes{
    height: 160px;
}
/*#region ANIMATION */
.slide-leave-active,
  .slide-enter-active {
    
    position: absolute;
    top: 56px;
    transition: 1s;
    width: 380px;
  }

  .slide-enter {
    transform: translate(-100%, 0);
    transition: opacity .5s;
  }

  .slide-leave-to {
    opacity:0;
    transform: translate(100%, 0);
  }

  .slide-right-leave-active,
  .slide-right-enter-active {
    position: absolute;
    top: 56px;
    transition: 1s;
    width: 380px;
  }

  .slide-right-enter {
    background: blue;
    transform: translate(100%, 0);
    transition: opacity .5s;
  }

  .slide-right-leave-to {
    opacity:0;
    transform: translate(-100%, 0);
  }
/*#endregion ANIMATION */

</style>>