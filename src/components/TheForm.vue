<template>
    <form class="x" action="#">
        <h1  class="text-left">{{frmName}}</h1>
        <InputBox placeholder="Email" label="Email:" />
        <InputBox placeholder="Subject" label="Subject:" />
        <InputBox placeholder="Message" label="Message:" id="mess" />
        <PlayButton 
        :btnclass="btnClass"
        :label="btnLabel"
        @le-button-click="play"
         />
    </form>
</template>

<script>
import InputBox from './InputBox.vue'
import PlayButton from './PlayButton.vue'

    export default{
        data: function(){
            return{
                 btnClass: 'form-control btn btn-primary',
                 btnLabel: 'Submit'
            }
        },
        name: 'TheForm',
        components: { InputBox, PlayButton },
        props:{
            frmName: String
        },
        methods:{
            play(){
                console.table(this.frmName)
            }
        }
    }
</script>