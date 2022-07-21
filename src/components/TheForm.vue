<template>
    <form :class="frmClass" action="#" :id="frmId">
    <InputBox 
            v-for="input in inputs" 
            :key="input[0].input"
            :placeholder="input[0].input" 
            :label="input[0].input"
            v-model="val[0]"
            :id="input[0].input.toLowerCase()"
            :theValue="input[0].val"
            @key-is-up="$emit('key-is-up', val[0].value)"/> 
       {{val[0]}}
    <PlayButton 
           v-for="btn in btns" 
           :key="btn"
           :label="btn[0].btnLabel"
           :btnclass="btn[0].btnClass"
            @le-button-click="play(btn[0].btnLabel)"/>
    </form>
</template>

<script>

import InputBox from './InputBox.vue'
import PlayButton from './PlayButton.vue'


    export default{
      
        name: 'TheForm',
        data: function(){
            return{
                val: ['']
            }
        },
        components: { InputBox, PlayButton },
        props:{
            frmName: String,
            frmId: String,
            frmClass: String,
            inputs: Array,
            btns: Array,
        },
        methods:{
            play(value){
                console.table(value)
            
            },
            theMessage(e){
                this.val = this.val + inputs[0].value
            }
            
        }
    }
</script>