<template>
  <div class="container2">
    <ul class="information">
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

      <br>
      <label for="m_name">관리담당자:</label>
      <select id="m_name" v-model="selectedManagerName" @input="changingManagerName($event)">
        <option v-for="manager in ManagerData" :key="manager.m_id" :value="manager.m_name">
          {{ manager.m_name }}
        </option>
      </select>
      <br>
      <label for="dept">**부서:</label>
      <input :disabled="step_dis == 10" type="text" id="dept" v-model="myManager.dept">
      <br>
      <label for="position">**직위:</label>
      <input :disabled="step_dis == 10" type="text" id="position" v-model="myManager.position">
      <br>
      <label for="m_phone">**연락처:</label>
      <input :disabled="step_dis == 10" type="text" id="m_phone" v-model="myManager.phone">
    </ul>
    <div id="message">고객 관리 담당자를 지정하세요!!!</div>
  </div>

  <ModalVue :CustomerData="CustomerData"></ModalVue>
</template>

<script>
import ManagerData from '../assets/manager.js';
import ModalVue from './modal.vue';


export default {
  name: 'InformationVue',
  data() {
    return {
      ManagerData: ManagerData,
      step_dis: 10,
      selectedManagerName: '강하게',
      managerName : '',
    };
  },
  components: {
    ModalVue,
  },
  props: {
    CustomerData: Array,
    myPicked: Number,
    copyCustomerData: Array,
    step : Number,
    changeStatus : Boolean,
  },
  computed: {
    localMember() {
      // Ensure copyCustomerData is defined and is an array
      if (Array.isArray(this.copyCustomerData)) {
        return this.copyCustomerData.find(customer => customer.cus_id === this.myPicked) || {};
      }
      return {}; // Return an empty object if CustomerData is not an array
    },

    myManager() {
      // Find manager by m_name which matches the selectedManagerName
      if (this.selectedManagerName) {
        return this.ManagerData.find(manager => manager.m_name === this.selectedManagerName) || {};
      }
      return {}; // Return empty object if no selectedManagerName
    },
  },
  watch: {
    localMember(newValue) {
      
      if (newValue.m_id) {
      // newValue.m_id가 설정된 경우, m_id에 해당하는 매니저를 찾아서 selectedManagerName을 설정
        const manager = this.ManagerData.find(manager => manager.m_id === newValue.m_id);
        if (manager) {
          this.selectedManagerName = manager.m_name;
        } else {
          this.selectedManagerName = '';
        }
      }
      else{
        this.selectedManagerName = '';
      }
    
   }
      
  },

  methods: {
    changingManagerName(event) {
      if(this.changeStatus){
        console.log(this.changeStatus)
        const manager = this.ManagerData.find(manager => manager.m_name === event.target.value);
        this.localMember.m_id = manager.m_id;
       // console.log(event.target.value)
      }
    },
    // Customer
    changingCustomerName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.cus_name = event.target.value;
      }
    },
    changingEmailName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.email = event.target.value;
      }
    },
    changingTelName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.tel = event.target.value;
      }
    },
    changingPhoneName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.phone = event.target.value;
      }
    },
    changingJobName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.job = event.target.value;
      }
    },
    changingAddrName(event){
      if(this.changeStatus){
        // console.log(this.changeStatus)
        this.localMember.addr = event.target.value;
      }
    },   

  }
 


};
</script>

<style>
/* Add your styles here */
</style>