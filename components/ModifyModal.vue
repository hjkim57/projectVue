<template>
    <div class="modify-bg" v-if="modifyStatus==true">
        <div class="modify-white-bg">
            <CustomerVue></CustomerVue> 
            <InformationVue></InformationVue>
            <button id="modify" @click="modify">변경</button>
        </div>
    </div>
  
</template>

<script>

import CustomerVue from './Customer.vue';
import InformationVue from './Information.vue';

export default {
    name : 'ModifyModal',
    data() {
        return {
            
        }
    },
    components: {
        InformationVue,
        CustomerVue,
    },
    props : {
        modifyStatus : Boolean,
        step : Number,
    },
    methods: {
        modify(){
            console.log(this.modifyStatus)
            this.$emit('CloseModify');
        }
    },
}
</script>

<style>
    body {
        margin : 0;
    }
    div {
        box-sizing: border-box;
    }
    .modify-bg {
        margin-left: 350px;
        width: 500px; height:600px;
        background: rgba(0,0,0,0.5);
        position: fixed; padding: 20px;
    }
    .modify-white-bg {
        width: 100%; 
        height: 500px;
        background: white;
        border-radius: 8px;
        padding: 20px;
    } 
    .modify-white-bg label {
        display: inline-block;
        width: 150px;
        text-align: right;
        margin-right: 0px;
        margin-left: 0px;
    }
</style>