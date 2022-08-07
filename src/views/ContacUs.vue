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
                [{input: 'Subject', val: '', type: 'text', errMsg:''}]
            ],
            
            textAreas:  [
                [{ 
                    input: "Message",
                    label: "Message",
                    theId : "alf-msg", 
                    name : "alf-msg", 
                    rows : 4, 
                    cols : 50, 
                    val: '', 
                type:'textarea', 
                errMsg:''}]
                ],
            
            btns: [
                [{btnClass: 'form-control btn btn-primary',btnLabel: 'Submit'}]
                ]

        }
    }
}
</script>
