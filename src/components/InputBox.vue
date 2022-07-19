<template>
<div class="row">
    <div class="form-group col-md-6 mx-auto">
        <label :for="theId">{{label}} {{theId}}</label>
        <input class="form-control" 
        type="text" name="" 
        :id="theId"
        :placeholder="label">
    </div>
   
</div>
</template>

<script>
    export default{
        name: 'InputBox',
        props: {
            label: String,
            txtClass: String,
            theId: String
        }
    }
</script>