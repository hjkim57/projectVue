<template>
    <div class="black-bg" v-if="modalStatus==true">
    <div class="white-bg">
        <ul class="information">
            <label for="c_date">**작성일자:</label>
            <input type="date" id="c_date" v-model="newMember.create_date">
            <br>
            <label for="c_name">*고객명:</label>
            <input type="text" id="c_name" v-model="newMember.cus_name">
            <br>
            <label for="c_jm_number">*실명번호:</label>
            <input type="text" id="c_jm_number" v-model="newMember.jumin_id">
            <br>
            <label for="c_email">*E-mail:</label>
            <input type="email" id="c_email" v-model="newMember.email"> 
            <br>
            <label for="c_home_call">전화번호:</label>
            <input type="text" id="c_home_call" v-model="newMember.tel"> 
            <br>
            <label for="c_phone_call">*핸드폰 번호:</label>
            <input type="text" id="c_phone_call" v-model="newMember.phone"> 
            <br>
            <label for="job">*직업:</label>
            <input type="text" id="job" v-model="newMember.job"> 
            <br>
            <label for="c_address">주소:</label>
            <input type="text" id="c_address" v-model="newMember.addr"> 
            <br>
        </ul>
      <button @click="submitMember">저장</button>
    </div>
   </div>

   <!-- <CounselVue :newMember="newMember" /> -->

</template>

<script>

// import CounselVue from './counsel.vue';

export default {
    name : 'ModalVue',
    components : {
        // CounselVue,
    },
    props : {
        modalStatus : Boolean,
        CustomerData : Array,
    },
    data() {
        return {
            newMember : {
                cus_id:'',
                create_date: '',
                cus_name: '',
                jumin_id: '',
                email: '',
                tel: '',
                phone: '',
                job: '',
                addr: '',
                m_id: 0,
            }
        }
    },

    methods :{
        submitMember(){
            // console.log(this.newMember)
            // if (Array.isArray(this.CustomerData)) {
            //     this.newMember.cus_id = this.CustomerData.length + 1;
            // } else {
            //     console.error('CustomerData is not an array or is undefined');
            //     this.newMember.cus_id = 1; // Default value if CustomerData is not valid
            // }
            // this.newMember.cus_id = this.CustomerData.length
            this.$emit('newMember',this.newMember)
            this.$emit('CloseModal')
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

    .information {

        display: inline-block;
    width: 100px;
    text-align: right;

    }
    .information label {
    display: inline-block;
    width: 100px;
    text-align: right;
    margin-right: 5px;
    margin-left: 10px;
}
</style>