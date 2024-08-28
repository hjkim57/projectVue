<template>
    <div class="black-bg" v-if="modalStatus==true">
    <div class="white-bg">
        <ul class="information">
            <label for="c_date">**작성일자:</label>
            <input type="text" id="c_date">
            <br>
            <label for="c_name">*고객명:</label>
            <input type="text" id="c_name">
            <br>
            <label for="c_jm_number">*실명번호:</label>
            <input type="text" id="c_jm_number"> 
            <br>
            <label for="c_email">*E-mail:</label>
            <input type="email" id="c_email"> 
            <br>
            <label for="c_home_call">전화번호:</label>
            <input type="text" id="c_home_call"> 
            <br>
            <label for="c_phone_call">*핸드폰 번호:</label>
            <input type="text" id="c_phone_call"> 
            <br>
            <label for="job">*직업:</label>
            <input type="text" id="job"> 
            <br>
            <label for="c_address">주소:</label>
            <input type="text" id="c_address"> 
            <br>
        </ul>
      <button v-on:click="$emit('CloseModal')">닫기</button>
    </div>
   </div>
</template>

<script>
// import InformationVue from './Information.vue';

export default {
    name : 'ModalVue',
    components : {
        // InformationVue,
    },
    props : {
        modalStatus : Boolean,
        CustomerData : Array,
    }

}
</script>

<style>
    body {
        margin : 0;
    }
    div {
        box-sizing: border-box;
    }
    .black-bg {
        width: 50%; height:100%;
        background: rgba(0,0,0,0.5);
        position: fixed; padding: 20px;
    }
    .white-bg {
        width: 100%; background: white;
        border-radius: 8px;
        padding: 20px;
    } 
    button {
        float: ;
    }
</style>