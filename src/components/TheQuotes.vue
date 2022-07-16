<template>
    <div class="container">
    <div class="header-space"></div>        
        <input disabled v-model="searchQuote" type="text">
        <p>{{searchQuote}}</p>
        <p v-if="quoteId === 1">{{quoteId}}</p>
        <div v-for="item in quotes" :key="item">
            <h1 >{{item.title}}</h1>
             <h2 class="text-secondary">{{item.quote}}</h2>
            <h2 class="text-primary text-align-right">{{item.author}}</h2>
        </div>

        
    </div>
</template>

<script>

import quotesData from '../../public/quotes.json'

    export default{
        name: 'TheQuotes',
        data: function(){
            return{
                quotes: quotesData,
                searchQuote: 'x',
                quoteId: 1
            }
        },
        computed: {
            filterQuotes: function(){
                this.searchQuote = this.quotes[this.quoteId].title;
                return this.searchQuote;
            }
        },

        methods: {
     randomQuote(){
              // check if already an interval has been set up
              if (!nIntervId) {
                nIntervId = setInterval(this.filterQuotes, 1000);
              }
              return 0;
            }

        }
   
    }
</script>

<style scoped>
.header-space{
  margin-top: 4rem;
}

</style>>