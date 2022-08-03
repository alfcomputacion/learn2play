<template>
<div class="row">
    <div class="form-group col-12 mx-auto">
        <label :for="label.toLowerCase()">{{label}} {{theId}}</label>
        <input class="form-control" 
        ref="miCampo"
         :name="label" 
         :type="type"
         :errorMsg="errorMsg"
        :id="label.toLowerCase()"
        :placeholder="label"
        :value="theValue"
       @input="$emit('update:modelValue', $event.target.value)"
       @keyup="$emit('key-is-up', $event.target.value)">
    </div>
    
   <!--  {{theValue}} -->
    <div  v-if="errorMsg" class="form-group col-12 mx-auto">
        <p class="text-danger" >{{errorMsg}}</p>
    </div>
   <!--todo theValue could be conflictin with other component -->
</div>
</template>

<script>
    export default{
        name: 'InputBox',
        props: {
            label: String,
            txtClass: String,
            theId: String,
            theValue: String,
            type: String,
            errorMsg: String
        }
    }
</script>