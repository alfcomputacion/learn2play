<template>
     <div class="container m-auto"> 
        <div class="header-space"></div>  
        <article class="a-login" id="a-login"></article>
        <!--#region MAIN -->
        <div id="m-login" class="main"> 
        <section v-if="!show" class="row mx-1 my-3" id="login-div-form">
            <h1>Log in</h1>
              <form action="#" method="post" id="login-form">
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
            @key-is-up="$emit('key-is-up', val[0].value)" 
           /> 
<PlayButton :label="logbtn[0].btnLabel" :btnclass="logbtn[0].btnClass" />
                <input id="btn-login" type="button" value="Login">
                <a @click="show = true" id="register-link" href="#">Need an account? <em class="msg">Register</em> </a>
            </form>
      
        </section>

        <section v-if="show" class="row mx-1 my-3" id="register-div-form">
            <h1>Register</h1>
            <form action="#" method="post" id="register-form">
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
            @key-is-up="$emit('key-is-up', val[0].value)" 
            /> 

             
                <div id="gamer">
                    <input type="checkbox" id="gamerCh" required>
                    <label for="gamerCh">I am over 13 and like playing games.</label>
                </div>
            <PlayButton :label="regbtn[0].btnLabel" :btnclass="regbtn[0].btnClass" />
                <input id="btn-register" type="button" value="Register">
             <a @click="show = false" id="login-link" href="#">Have an account? <em class="msg">Login</em></a>
            </form>
           
        </section>
        </div> 
        <!--#endregion MAIN -->
    </div>
</template>

<script>
import InputBox from './InputBox.vue'
import PlayButton from './PlayButton.vue'
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
                [{input:'Email', val: 'a', type: 'email', errMsg:'', required: true, 
                pattern: "\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})",
                placeholder: "example@company.com"}],
                [{input: 'Password', val: '', type: 'password', errMsg:''}],
                [{input: 'RepPassword', val: '', type: 'password', errMsg:''}]
            ],
            logbtn: 
                 [{btnClass: 'form-control btn btn-primary',btnLabel: 'Log in'}],
            regbtn:  
              [{btnClass: 'form-control btn btn-warning',btnLabel: 'Register'}]
                
        }
    },
    show: false,
    components: { InputBox, PlayButton }
}
</script>