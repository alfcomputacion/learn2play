<template>
 <div id="m-login" class="main m-t-4 form-control">
    <div class="header-space"></div>    
         <TheForm frmName="Contact us"/>
    </div> 
</template>

<script>
import InputBox from './InputBox.vue';
import TheForm from './TheForm.vue';
    export default{
    name: "ContactUs",
    components: { InputBox, TheForm },
    data: function(){
        return{
            lblEmail: 'Email',
            lblSubject: 'Subject',
            lblMessage: 'Message'
        }
    }
}
</script>