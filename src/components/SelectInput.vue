<template>
<div class="container row mx-1 my-3">
    <label class="col font-weight-bold" :for="id">{{label}}</label>
        <select :id="id"
            class="col form-control"
            :value="currentValue"
            @input="$emit('update:modelValue', $event.target.value)">
            <option 
                v-for="option in options" 
                :key="option[1]"
                :value="option[1]">
                {{option[0]}}
            </option>
        </select>
         
</div>
  
</template>

<script>
    export default{
        name: 'SelectInput',
        props:{
            label: String,
            id: String,
            options: Array,
            currentValue: String
        }
    }
</script>
<style scoped>
    .container{
        margin-top: .5rem;
    }    
    label{
        padding-right: .5rem;
    }
</style>>
