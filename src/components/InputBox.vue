<template>
<div class="row">
    <div class="form-group col-md-6 mx-auto">
        <label :for="label">{{label}} {{theId}}</label>
        <input class="form-control" 
        type="text" name="label" 
        :id="label"
        :placeholder="label"
        :value="theValue"
       @input="$emit('update:modelValue', $event.target.value)">
    </div>
   <!--todo theValue could be conflictin with other component -->
</div>
</template>

<script>
    export default{
        name: 'InputBox',
        data: function(){
            return{
                theValue: null
            }
        },
        props: {
            label: String,
            txtClass: String,
            theId: String,
            theValue: String
        }
    }
</script>