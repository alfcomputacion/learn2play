<template>
  <div class="container">
    <TheHeader @goto-page="changePage" />
       
        <div v-if="page === 'mathificent'" class="mathificent">
          <TheMathificent />
        </div>

        <div v-else-if="page === 'anagram'" class="anagram">
          <AnagramHunt />
        </div>      
        <div  v-else-if="page === 'home'">
          <div class="header-space"></div>
          <TheQuotes  />
          
          <h2>Home </h2>
        </div>

  </div>
</template>

<script>

import TheMathificent from './TheMathificent.vue';
import TheHeader from './TheHeader.vue';
import AnagramHunt from './AnagramHunt.vue';
import TheQuotes from './TheQuotes.vue';

export default {
  name: 'App',
  data: function(){
    return{
      page: 'home'
    }
  },
  methods:{
    changePage(value){
    this.page = value
    }
  },
  
  components: {
    TheMathificent,
    TheHeader,
    AnagramHunt,
    TheQuotes
}
}
</script>

<style scoped>
.header-space{
  margin-top: 4rem;
}

</style>>