<template>
     <div class="container"> 
        <div class="header-space"></div>  
      
<section v-if="!show"  id="login-div-form" >
            <h1>Log in</h1>
    <form action="#" method="post" id="login-form"  @submit.stop.prevent="prevent">
        <InputBox 
                    v-for="input in logInputs" 
                    :key="input[0].input"
                    :placeholder="input[0].placeholder" 
                    :label="input[0].input"
                    v-model="input[0].val"
                    :id="input[0].input.toLowerCase()"
                    :theValue="input[0].val"
                    :type="input[0].type"
                    :errorMsg="input[0].errMsg"
                    @key-is-up="updateErr(input[0])" 
           /> 
        <PlayButton :label="logbtn[0].btnLabel" 
                    :btnclass="logbtn[0].btnClass" 
                    @le-button-click="submitLogIn(logbtn[0].btnLabel)"/>
        <!-- <input id="btn-login" type="button" value="Login"> -->
                <a @click="show = true" id="register-link" href="#">Need an account? <em class="msg">Register</em> </a>
    </form>
</section>

<section v-if="show"  id="register-div-form">
            <h1>Register</h1>
    <form action="#" method="post" id="register-form"  @submit.stop.prevent="prevent">
            <InputBox 
                    v-for="input in regInputs" 
                    :key="input[0].input"
                    :placeholder="input[0].placeholder" 
                    :label="input[0].input"
                    v-model="input[0].val"
                    :id="input[0].input.toLowerCase()"
                    :theValue="input[0].val"
                    :type="input[0].type"
                    :errorMsg="input[0].errMsg"
                   @key-is-up="updateErr(input[0])" 
            /> 
  <template  v-if="!isPassMatch" class="form-group col-12 mx-auto">
        <p class="text-danger" >Passwords do not match</p>
    </template>
             
                <div id="gamer">
                    <input type="checkbox" id="gamerCh"
                    @change="isChecked = !isChecked">   
                    <label class="ml-2" for="gamerCh">I am over 13 and like playing games.</label>
                </div>
                <!-- !todo NEED FIX IS CHECKED  -->
                 <template  v-if="!isChecked" class="form-group col-12 mx-auto">
                     <p class="text-danger" >You need to confirm you are at least 13 years old</p>
                </template>
            <PlayButton :label="regbtn[0].btnLabel" :btnclass="regbtn[0].btnClass" 
                @le-button-click="submitLogIn(regbtn[0].btnLabel)"/>
            <!-- <input id="btn-register" type="button" value="Register"> -->
             <a  @click="show = false" id="login-link" href="#">Have an account? <em class="msg">Login</em></a>
    </form>
</section>
        </div> 
        <!--#endregion MAIN -->

</template>

<script>
import InputBox from '../components/InputBox'
import PlayButton from '../components/PlayButton.vue'
export default {
    name: "LogSignIn",
    data() {
        return {
            show: false,
            logInputs: [
                [{input:'Email', val: '', type: 'email', errMsg:'', required: true, 
                pattern: "\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})",
                placeholder: "example@company.com"}],
                [{input: 'Password', val: '', type: 'password', errMsg:''}]
            ] ,
            regInputs: [
                [{input:'Email', val: '', type: 'email', errMsg:'', required: true, 
                pattern: "\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})",
                placeholder: "example@company.com"}],
                [{input: 'Password', val: '', type: 'password', errMsg:''}],
                [{input: 'RepPassword', val: '', type: 'password', errMsg:''}]
            ],
            isPassMatch: false,
            isChecked: true,
            logbtn: 
                 [{btnClass: 'btn btn-primary form-control col-12 mb-3',btnLabel: 'Log in'}],
            regbtn:  
              [{btnClass: 'btn btn-danger form-control col-12 mb-3',btnLabel: 'Register'}],
            
            submitted: false,
            logErrorDetected: false,
            regErrorDetected: false
        }
    },
    methods:{
    submitLogIn(e){
                // alert('Submitted by: '+e)
              
                this.submitted = true
                this.logErrorDetected = []
                this.regErrorDetected = []
                
                switch (e) {
                    case 'Log in':
                        //  this.logInputs[0][0].errMsg = 'Email must be a valid email exmaple@mail.com'
                        let verifiedEmail = this.validateEmail(this.logInputs[0][0])
                        let verifiedPass = this.validatePassword(this.logInputs[1][0]) 
                       if( verifiedPass && verifiedEmail)
                        {
                        alert('You are now Logged in as:  ' + this.logInputs[0][0].val)
                            this.logInputs[0][0].val = ''
                            this.logInputs[1][0].val = ''
                        }
                        break;
                    case 'Register':
                      let verRegEmail =  this.validateEmail(this.regInputs[0][0])
                      let verRegPass =  this.validatePassword(this.regInputs[1][0])
                      let verRegPass2 = this.validatePassword(this.regInputs[2][0])
                      let checked13 = document.getElementById('gamerCh')
                      
                    //   let passMatch = this.passordMatch(this.regInputs[1][0].val, this.regInputs[2][0].val)
                      this.isPassMatch = this.regInputs[1][0].val === this.regInputs[2][0].val 
                      
                        if(verRegEmail && verRegPass && verRegPass2 && this.isPassMatch && checked13){
                            alert('You have been registered as ' + this.regInputs[0][0].val)
                            this.regInputs[0][0].val = ''
                            this.regInputs[1][0].val = ''
                            this.regInputs[2][0].val = ''
                            checked13.checked = false
                        }
                        
                        
                        break;
                
                    default:
                        break;
                }

            },
    updateErr(e){
                console.log('update error from: ' + e.input)
    if( this.submitted){ 
        switch (e.input) {
            case 'Email':
                this.validateEmail(e)
                break;
            case 'Password':
               this.validatePassword(e)
               break;
            case 'RepPassword':
               this.validatePassword(e)
                break;
                default:
                break;
        }
    }
        },
        validateEmail(email){
            console.log('este es email from: ' +email.input)
                if(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})$/.test(email.val)){
                    console.log('x')
                    if(!this.show){
                          this.logInputs[0][0].errMsg = ''
                        
                    }else{
                          this.regInputs[0][0].errMsg = ''
                    }
                  return true
                    // e.errMsg = ''
                }else{
                    console.log('y')
                    if(!this.show){
                         this.logInputs[0][0].errMsg = 'Validate email exmaple@mail.com'
                    }else{

                        this.regInputs[0][0].errMsg = 'Validate email exmaple@mail.com'
                    }
                 return false
                }
        },
        validatePassword(pass){
           if(pass.val.length >= 5){
               this.isPassMatch = this.regInputs[1][0].val === this.regInputs[2][0].val
                    pass.errMsg = ''
                    return true
                } else {
                    pass.errMsg = 'Password needs to be 5 or more char long'
                    return false
                }
        },

    },
  
    components: { InputBox, PlayButton }
}
</script>
<style scoped>
.container{
    margin: 0 auto;
    width: 380px;
}
.msg{
    color: rgba(105, 201, 245, 0.768);
    text-shadow: 0 0 0.01rem black;
}
</style>