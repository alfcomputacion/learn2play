<template>
<div class="row">
    <div class="col-12 text-center p-2">
     <button 
        :class="btnclass"
        @click="$emit('le-button-click')">
        {{label}}
    </button>
    </div>
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