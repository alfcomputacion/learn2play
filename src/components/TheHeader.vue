<template>
<nav class="navbar navbar-dark bg-primary navbar-expand-md fixed-top">
  <a class="navbar-brand" href="#page-top">
    <span class="d-md-nonesss">ALFCOMPUTACION</span>
  </a>
    <button class="navbar-toggler" type="button"
      data-toggle="collapse"
      data-target="#navbar-content"><span class="navbar-toggler-icon"></span>
    </button>
    
    <div class="collapse navbar-collapse" id="navbar-content">
      <ul class="navbar-nav">
        <li class="navbar-item">
          <a
          id="home" 
          data-toggle="collapse"
          data-target="#navbar-content" 
      @click="$emit('goto-page','home')" href="#" class="nav-link">Home</a>
        </li>
        <li class="navbar-item dropdown">
          <a href="#" class="nav-link dropdown-toggle" role="button"
          id="navbar-dropdown" data-toggle="dropdown">Games</a>
                <div class="dropdown-menu">
                    <a
                      id="mathificent" 
                      data-toggle="collapse"
                       data-target="#navbar-content" 
                       @click="$emit('goto-page', 'mathificent')" 
                       href="#" 
                       class="dropdown-item">Mathificent</a>
                    <a
                      id="anagram" 
                      data-toggle="collapse"
                       data-target="#navbar-content" 
                       @click="$emit('goto-page', 'anagram')" 
                       href="#" 
                       class="dropdown-item">Anagram</a>
                </div>
        </li>
        <li class="navbar-item">
          <a
          id="log-in" 
          data-toggle="collapse"
          data-target="#navbar-content" 
      @click="$emit('goto-page','login')" href="#" class="nav-link">Log in</a>
        
        </li>
          <li class="navbar-item">
          <a
          id="contact-us" 
          data-toggle="collapse"
          data-target="#navbar-content" 
          @click="$emit('goto-page','contactus')" href="#" class="nav-link">Contact Us</a>
        </li>

         <li class="navbar-item">
          <a
          id="about-us" 
          data-toggle="collapse"
          data-target="#navbar-content" 
          @click="$emit('goto-page','aboutus')" href="#" class="nav-link">About Us</a>
        </li>
      </ul>
    </div>
   
</nav>  

</template>

<script>
    export default{
        name: 'TheHeader',
        data: function(){
          return{
            isMobile: 0
          }
        },
        methods:{
          //Avoids collapse
          changeDataSets(){
              this.isMobile = window.innerWidth
              let homeLink = document.getElementById('home') 
              let mathificentLink = document.getElementById('mathificent') 
              let anagramLink = document.getElementById('anagram') 
              let logInLink = document.getElementById('log-in') 
              let aboutUsLink = document.getElementById('about-us') 
              let contactUsLink = document.getElementById('contact-us') 
            if(this.isMobile > 767){
              anagramLink.dataset.toggle = ''
              mathificentLink.dataset.toggle = ''
              homeLink.dataset.toggle = ''
              logInLink.dataset.toggle = ''
              aboutUsLink.dataset.toggle = ''
              contactUsLink.dataset.toggle = ''
            }else{
              anagramLink.dataset.toggle = 'collapse'
              mathificentLink.dataset.toggle = 'collapse'
              homeLink.dataset.toggle = 'collapse'
              logInLink.dataset.toggle = 'collapse'
              aboutUsLink.dataset.toggle = 'collapse'
              contactUsLink.dataset.toggle = 'collapse'
            }
          }
        },
    
        mounted(){
          this.changeDataSets()
           window.addEventListener('resize', this.changeDataSets())
          }
      
         }

</script>