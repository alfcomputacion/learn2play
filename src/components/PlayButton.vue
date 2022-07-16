<template>
<div class="row mx-1 my-3">
     <button 
        :class="[btnclass]"
        @click="$emit('le-button-click')">
        {{label}}
    </button>
</div>
   
</template>

<script>
export default{
    name: 'PlayButton',
    props:{
        btnclass: String,
        label: String
    }
}
</script>