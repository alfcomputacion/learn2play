<template>
    <footer>
<nav class="bottom-nav fixed-bottom text-center text-white">
        <div class="social">
            <a @click="$emit('goto-page', 'contactus')" href="#"><i class="fa fa-envelope fa-2x  p-4" aria-hidden="true"></i></a>
            <a href="https://twitter.com/"><i class="fab fa-twitter fa-2x  p-4"></i></a>
            <a href="https://www.facebook.com/"><i class="fab fa-facebook fa-2x  p-4"></i></a>
            <a href="https://www.instagram.com/"><i class="fab fa-instagram fa-2x  p-4"></i></a>
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
        background: darkblue;
        width: 100vw;
    }
    .social a,.logo a{
        color: white;
    }
    .social a:active,.logo a:active {
        color: rgb(138, 131, 131);
    }
    

</style>