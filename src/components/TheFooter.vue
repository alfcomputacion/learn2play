<template>
    <footer>
<nav class="bottom-nav text-center">
        <div class="social">
            <a @click="$emit('goto-page', 'contactus')" href="#"><i class="fa fa-envelope fa-2x  p-4" aria-hidden="true"></i></a>
            <a href="https://twitter.com/alfcomputacion"><i class="fab fa-twitter fa-2x  p-4"></i></a>
            <a href="https://www.facebook.com/jose.rosas.7737"><i class="fab fa-facebook fa-2x  p-4"></i></a>
            <a href="https://www.instagram.com/alfcomputacion/"><i class="fab fa-instagram fa-2x  p-4"></i></a>
        </div>
        <div id="l-index" class="logo">
            <a title="Home Page" href="index.html">&copy;2019 ALFCOMPUTACION</a>
        </div>  
</nav>
   <!-- ! Logo -->
   
</footer>
</template>

<script>
    export default{
        name: 'TheFooter'
    }
</script>

<style scoped>
    .bottom-nav{
        margin-bottom: 0;
        background: navy;
        width: 100vw;
    }
</style>