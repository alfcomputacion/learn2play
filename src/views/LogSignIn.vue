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

             
                <div id="gamer">
                    <input type="checkbox" id="gamerCh" required>   
                    <label class="ml-2" for="gamerCh">I am over 13 and like playing games.</label>
                </div>
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
                console.log(this.passordMatch('a','a'))
                this.submitted = true
                this.logErrorDetected = []
                this.regErrorDetected = []
                
                switch (e) {
                    case 'Log in':
                        //  this.logInputs[0][0].errMsg = 'Email must be a valid email exmaple@mail.com'
                        this.validateEmail(this.logInputs[0][0])
                        alert('submitted by Login' + this.logInputs[0][0].val)
                        break;
                    case 'Register':
                        this.validateEmail(this.regInputs[0][0])
                        alert('submitted by Register')
                        
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
                if(e.val.length > 5){
                    e.errMsg = ''
                } else {
                    e.errMsg = 'Password needs to be 5 char long'
                }
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
                  
                    // e.errMsg = ''
                }else{
                    console.log('y')
                    if(!this.show){
                         this.logInputs[0][0].errMsg = 'Validate email exmaple@mail.com'
                    }else{

                        this.regInputs[0][0].errMsg = 'Validate email exmaple@mail.com'
                    }
                    // e.errMsg = 'Email must be valid email exmaple@mail.com'
                }
        },
        passordMatch(pass, passTwo){return pass === passTwo }

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