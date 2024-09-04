<template>
    <div class="black-bg" v-if="modalsearchStatus==true">
    <div class="white-bg">
        <ul class="information_2">
            
            <fieldset class="names_m">
            <label v-for="mem in copyManagerData" :key="mem.m_id">
            <input type="radio" name="managers" :value="mem.m_id" v-model="myPick_manager" />
            {{ mem.m_name }}<br>
            </label>
            <button @click="closeModalsearch">닫기</button>
            </fieldset>
            
            <fieldset class="names_c">
            <label v-for="mem in copyCustomerData" :key="mem.cus_id">
            <input :disabled="mem.m_id != myPick_manager" type="radio" name="customers" :value="mem.cus_id" v-model="myPick_cus" />
            {{ mem.cus_name }}<br>
            </label>
            </fieldset>

            <label for="c_date">**작성일자:</label>
            <input :disabled="step_dis == 10" type="date" id="c_date" v-model="localMember.create_date">
            <br>
            <label for="c_name">*고객명:</label>
            <input type="text" id="c_name" v-model="localMember.cus_name" @input="changingCustomerName($event)">
            <br>
            <label for="c_jm_number">*실명번호:</label>
            <input type="text" id="c_jm_number" v-model="localMember.jumin_id">
            <br>
            <label for="c_email">*E-mail:</label>
            <input type="email" id="c_email" v-model="localMember.email" @input="changingEmailName($event)">
            <br>
            <label for="c_home_call">전화번호:</label>
            <input type="text" id="c_home_call" v-model="localMember.tel" @input="changingTelName($event)">
            <br>
            <label for="c_phone_call">*핸드폰 번호:</label>
            <input type="text" id="c_phone_call" v-model="localMember.phone" @input="changingPhoneName($event)">
            <br>
            <label for="job">*직업:</label>
            <input type="text" id="job" v-model="localMember.job" @input="changingJobName($event)">
            <br>
            <label for="c_address">주소:</label>
            <input type="text" id="c_address" v-model="localMember.addr" @input="changingAddrName($event)">
            <br>
            
      
        </ul>
    </div>
   </div>

   <ModalVue></ModalVue>

</template>

<script>
import CustomerData from '../assets/customer.js';
import ManagerData from '../assets/manager.js';
// import ModalVue from './modal.vue';
import ModalVue from './Modal.vue';

export default {
  name: 'ModalsearchVue',
  data() {
    return {
      ManagerData: ManagerData,
      copyManagerData: [...ManagerData],
      copyCustomerData: [...CustomerData],
      step_dis: 10,
      myPick_manager: 1,
      managerName : '',
      // myPick_cus : 1,
      //copyCustomerData: [...CustomerData],

      
    };
  },
  components: {
    ModalVue,
  },
  props: {
    //CustomerData: Array,
    // myPicked: Number,
    //copyCustomerData: Array,
    step : Number,
    changeStatus : Boolean,
    modalsearchStatus : Boolean,
  },
  computed: {
    localMember() {
      // Ensure copyCustomerData is defined and is an array
      if (Array.isArray(this.copyCustomerData)) {
        return this.copyCustomerData.find(customer => customer.m_id === this.myPick_manager) || {};
      }
      return {}; // Return an empty object if CustomerData is not an array
    },
  },

  methods: {
    
    closeModalsearch(){
      this.$emit('CloseModalsearch')
    },
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

    /* .information {

        display: inline-block;
    width: 100px;
    text-align: right;

    } */
    .information_2 label {
    display: inline-block;
    width: 100px;
    text-align: right;
    margin-right: 5px;
    margin-left: 10px;
}
</style>