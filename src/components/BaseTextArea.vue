<template>
<div class="row">
    <div class="form-group col-12 mx-auto">
      <label :for="id">{{label}}</label>

        <textarea 
        :placeholder="label" 
        :id="theId" 
        :name="label"
        :errorMsg="errorMsg" 
        :rows="rows" 
        :cols="cols"
        :value="theValue"
       @input="$emit('update:modelValue', $event.target.value)"
       @keyup="$emit('key-is-up', $event.target.value)">
        </textarea>
  
    </div>
      <template  v-if="errorMsg" class="form-group col-12 mx-auto">
        <p class="text-danger" >{{errorMsg}}</p>
    </template>

   <!--todo theValue could be conflictin with other component -->
</div>
</template>

<script>
    export default{
        name: 'BaseTextArea',
        props: {
            theId: String,
            label: String,
            input: String,
            txtClass: String,
            cols: Number,
            rows: Number,
            theValue: String,
            type: String,
            errorMsg: String
        }
    }
</script>

<style scoped>
    textarea{
        padding-left: .5rem;
        color: blue;
    }
</style>