<template>
  <div class="container">
    <TheHeader @goto-page="changePage" />
       <!-- We condition the page 
          any time page changes it goes 
               to the right page -->
        <div v-if="page === 'mathificent'" class="mathificent">
          <TheMathificent />
        </div>

        <div v-else-if="page === 'anagram'" class="anagram">
          <AnagramHunt />
        </div>      
        <div  v-else-if="page === 'home'">
          <div class="header-space"></div>
          <TheQuotes  @goto-page="changePage"/>
          
        </div>
      <div v-if="page === 'contactus'" class="contactus">
        <form action="">
          <ContacUs />
        </form>
      </div>
 
    <TheFooter @goto-page="changePage" />
  </div>
</template>

<script>

import TheMathificent from './TheMathificent.vue';
import TheHeader from './TheHeader.vue';
import AnagramHunt from './AnagramHunt.vue';
import TheQuotes from './TheQuotes.vue';
import TheFooter from './TheFooter.vue';
import ContacUs from './ContacUs.vue';

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
    TheQuotes,
    TheFooter,
    ContacUs
}
}
</script>

<style scoped>
.header-space{
  margin-top: 4rem;
}

</style>>