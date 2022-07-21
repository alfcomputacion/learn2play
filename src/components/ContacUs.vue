<template>
 <div id="m-login" class="main m-t-4 form-control">
    <div class="header-space"></div>    
         <TheForm 
         :frmClass="frmClass"
         :frmId="frmId" 
         :inputs="inputs" 
         frmName="Contact us"
        @key-is-up="inputs[0].value"
         :btns="btns"
         />
    </div> 
</template>

<script>

import TheForm from './TheForm.vue';
    export default{
    name: "ContactUs",
    components: { TheForm },
    data: function(){
        return{
            frmId: 'frm-contact-us',
            frmClass: 'frm-contact',
            inputs:[[{input:'Email', val: 'a'}],[{input: 'Subject', val: 'b'}], [{input:'Message', val: 'c'}]],
            
            btns: [
                [{btnClass: 'form-control btn btn-primary',btnLabel: 'Submit'}],
                [{btnClass: 'form-control btn btn-warning',btnLabel: 'Cancel'}]
                ]

        }
    }
}
</script>