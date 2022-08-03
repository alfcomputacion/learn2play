<template>
<div class="main-container">

    <form :class="frmClass" method="post" action="#" :id="frmId" @submit.stop.prevent="prevent">
    <InputBox 
            v-for="input in inputs" 
            :key="input[0].input"
            :placeholder="input[0].input" 
            :label="input[0].input"
            v-model="input[0].val"
            :id="input[0].input.toLowerCase()"
            :theValue="input[0].val"
            :type="input[0].type"
            :errorMsg="input[0].errMsg"
          @key-is-up="updateErr(input[0])"  
/> 
        
    
    <BaseTextArea 
            v-for="input in textAreas" 
            :key="input.theId"
            :name="input.name"
            :rows="input.rows"
            :cols="input.cols"

            /> 
       
    <PlayButton 
           v-for="btn in btns" 
           :key="btn"
           :label="btn[0].btnLabel"
           :btnclass="btn[0].btnClass"
            @le-button-click="bntClicked(btn[0].btnLabel)"/>
    </form>
</div>
</template>

<script>

import InputBox from './InputBox.vue'
import PlayButton from './PlayButton.vue'
import BaseTextArea from './BaseTextArea.vue'


    export default{
      
        name: 'TheForm',
        data: function(){
            return{
              inputsReturn: this.inputs,
              errorDetected: false,
              submitted: false  
            }
        },
        components: { InputBox, PlayButton, BaseTextArea },
        props:{
            frmName: String,
            frmId: String,
            frmClass: String,
            inputs: Array,
            textAreas: Array,
            btns: Array,
        },
        methods:{
            bntClicked(value, e){
                //this gives the value of email subject and message inputs
                //at submit
                //todo this.errormsg is not updating or is not reactive???
                this.submitted = true
                this.errormsg = []
                console.log('before any if ' + this.errormsg[0])
                if(this.inputsReturn[0][0].val.length < 5){
                    console.log('length: '  + this.inputsReturn[0][0].val.length)
                    this.inputsReturn[0][0].errMsg = 'Email-cant\'t be empty'
                   this.errorDetected = true
        
                }
                if(this.inputsReturn[1][0].val.length < 5){
                     console.log('length: '  + this.inputsReturn[1][0].val.length)
                    this.inputsReturn[1][0].errMsg = 'Subject cant\'t be empty'
                    this.errorDetected = true
                }
                if(this.inputsReturn[2][0].val.length < 5 ){
                    this.inputsReturn[2][0].errMsg = 'Message cant\'t be empty'
                     console.log('length: '  + this.inputsReturn[2][0].val.length)
                 
                   this.errorDetected = true 
                }

                if(this.errorDetected === true ){
                    
                    alert("Message was not sent, Please check your information ")
                   this.submitted = true
                   console.log('este es errorDetected: ' + this.errorDetected)
                }else{
            alert(
                'Email: ' + this.inputsReturn[0][0].val  +
               'Subject: ' + this.inputsReturn[1][0].val  +
                'Message: ' + this.inputsReturn[2][0].val + 'Data was sent Thank you...' )
                 this.submitted = false
                 console.log('este es errorDetected: ' + this.errorDetected)
                }
            },
          
            noDefault(e){
                e.preventDefault()
            },
            updateErr(e){
            if(this.submitted){

                let item = e.input
              switch (item) {
                  case 'Email':
                      if(e.val.length < 1){
                          console.log('length: '  + this.inputsReturn[0][0].val.length)
                    this.inputsReturn[0][0].errMsg = 'Email-cant\'t be empty'
                    // this.errormsg.push([{key: 'Email', error: 'Email-cant\'t be empty'}])
                    this.errorDetected = true
                    // console.log("Array " + this.errormsg[0].key)
                    console.log('after first if ' +  this.errormsg.key)
                }  else{
                    this.inputsReturn[0][0].errMsg = ''
                    this.errorDetected = false
                    
                }                
                    break;
                case 'Subject':
                    if(e.val.length < 5){
                        console.log('length: '  + this.inputsReturn[1][0].val.length)
                    this.inputsReturn[1][0].errMsg = 'Subject cant\'t be empty'
                    this.errorDetected = true
                }  else{
                    this.inputsReturn[1][0].errMsg = ''
                   this.errorDetected = false
                }              
                    break;
                case 'Message':
                    if(e.val.length < 5){
                        console.log('length: '  + this.inputsReturn[2][0].val.length)
                    this.inputsReturn[2][0].errMsg = 'Message can\'t be empty'
                    console.log('el error de 2,0 ',this.inputsReturn[2][0].errMsg)
                    this.errorDetected = true
                    console.log('I found the message: ', this.inputsReturn[2][0].errMsg )    
                    // if( let temporal = this.errormsg.find(data => data.key === 'Message')){
                    //     data.error = 'Message cant\'t be empty'
                    //     // this.errormsg.push([{key: 'Message', error: 'Message cant\'t be empty'}])
                    // } 
                    
                }else{
                  this.inputsReturn[2][0].errMsg = ''
                  this.errorDetected = false
                }
              
                default:
                    break;
              }
                
                console.log (e.errMsg)
                    }//if submitted
            } ,
            checkErrors(object){
                    let item = object.input
                   
                       console.log(item)
                   

            }   
        },

        computed:{
            
        }
    }
</script>
<style scoped>
.main-container{
    margin: 0 auto;
    width: 380px;
}
</style>