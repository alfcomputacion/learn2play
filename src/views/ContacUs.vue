<template>
 <div id="m-login" class="main m-t-4 form-control">
    <div class="header-space"></div>    
         <TheForm 
         frmName="Contact us"
            :frmClass="frmClass"
            :frmId="frmId" 
            :inputs="inputs" 
            :textAreas="textAreas"

            :btns="btns"
         />
    </div> 
</template>

<script>

import TheForm from '@/components/TheForm.vue'
    export default{
    name: "ContactUs",
    components: { TheForm },
    data: function(){
        return{
            frmId: 'frm-contact-us',
            frmClass: 'frm-contact',
            inputs:[
                [{input:'Email', val: '', type: 'email', errMsg:''}],
                [{input: 'Subject', val: '', type: 'text', errMsg:''}], 
                [{input:'Message', val: '', type:'text', errMsg:''}]],
            
            textAreas:  [
                { 
                    label: "Message",
                    theId : "w3review", 
                    name : "w3review", 
                    rows : 4, cols : 50, 
                    theValue: '', 
                type:'textarea', 
                errMsg:'message-error'}
                ],
            
            btns: [
                [{btnClass: 'form-control btn btn-primary',btnLabel: 'Submit'}],
                [{btnClass: 'form-control btn btn-warning',btnLabel: 'Cancel'}]
                ]

        }
    }
}
</script>