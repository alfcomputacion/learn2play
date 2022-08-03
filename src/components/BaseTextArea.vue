<template>
<div class="row">
    <div class="form-group col-12 mx-auto">
      <label :for="id">{{label}}</label>

        <textarea :id="theId" :name="label" :rows="rows" :cols="cols">
        
        </textarea>

    </div>
 
   <!--todo theValue could be conflictin with other component -->
</div>
</template>

<script>
    export default{
        name: 'BaseTextArea',
        props: {
            theId: String,
            label: String,
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
        padding: 2px;
    }
</style>