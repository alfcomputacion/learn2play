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
          data-toggle="collapse"
          data-target="#navbar-content" 
      @click="$emit('goto-page','home')" href="#home" class="nav-link">Home</a>
        </li>
        <li class="navbar-item dropdown">
          <a href="#" class="nav-link dropdown-toggle" role="button"
          id="navbar-dropdown" data-toggle="dropdown">Games</a>
                <div class="dropdown-menu">
                    <a data-toggle="collapse"
                       data-target="#navbar-content" 
                       @click="$emit('goto-page', 'mathificent')" 
                       href="#mathificent" 
                       class="dropdown-item">Mathificent</a>
                    <a data-toggle="collapse"
                       data-target="#navbar-content" 
                       @click="$emit('goto-page', 'anagram')" 
                       href="#anagram" 
                       class="dropdown-item">Anagram</a>
                </div>
        </li>
      </ul>
    </div>
</nav>  

</template>

<script>
    export default{
        name: 'TheHeader'
        }

</script>