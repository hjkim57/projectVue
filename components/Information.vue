<template>
  <div class="container2">
    <ul class="information">
      <label for="c_date">**작성일자:</label>
      <input :disabled="step_dis == 10" type="date" id="c_date" v-model="localMember.create_date">
      <br>
      <label for="c_name">*고객명:</label>
      <input type="text" id="c_name" v-model="localMember.cus_name">
      <br>
      <label for="c_jm_number">*실명번호:</label>
      <input type="text" id="c_jm_number" v-model="localMember.jumin_id">
      <br>
      <label for="c_email">*E-mail:</label>
      <input type="email" id="c_email" v-model="selectedEmail" @input="changingEmail($event)">
      <br>
      <label for="c_home_call">전화번호:</label>
      <input type="text" id="c_home_call" v-model="selectedTel" @input="changingTel($event)">
      <br>
      <label for="c_phone_call">*핸드폰 번호:</label>
      <input type="text" id="c_phone_call" v-model="selectedPhone" @input="changingPhone($event)">
      <br>
      <label for="job">*직업:</label>
      <input type="text" id="job" v-model="selectedJob" @input="changingJob($event)">
      <br>
      <label for="c_address">주소:</label>
      <input type="text" id="c_address" v-model="selectedAddr" @input="changingAddr($event)">
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
import ModalVue from '../components/Modal.vue';


export default {
  name: 'InformationVue',
  data() {
    return {
      ManagerData: ManagerData,
      step_dis: 10,
      selectedManagerName: '강하게',
      managerName : '',
      name1 : null,
      name2 : null,
      selectedEmail: 'khg@gmail.com',
      selectedTel : '02-100-2000',
      selectedPhone : '010-1200-2300',
      selectedJob: '회사원',
      selectedAddr: '서울특별시 종로구 서대문로 123-3',
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
    newStatus : Boolean,
    newName : String,
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
      this.selectedEmail = newValue.email;
      this.selectedTel = newValue.tel;
      this.selectedPhone = newValue.phone;
      this.selectedJob = newValue.job;
      this.selectedAddr = newValue.addr;
      
   },
   changeStatus(newStatus) {
      console.log('Change Status updated to:', newStatus);
      this.secondStatus = newStatus;
      // 필요한 경우, changeStatus가 변경되었을 때 추가 작업 수행
    },  
      
  },

  methods: {
    changingManagerName(event) {
      setTimeout(() => {
        let manager = null;
        if (this.localMember.m_id != 0) {
          manager = this.ManagerData.find(manager => manager.m_id === this.localMember.m_id);
          this.name1 = manager.m_name;   
          // console.log("name1 : " + this.name1);     
        } else {
          // console.log("name1가 없습니다.")
        }
        this.name2 = event.target.value;
        // console.log("name2 : " + this.name2);

        if (this.newStatus) {
          const manager = this.ManagerData.find(manager => manager.m_name === this.name2);
          this.localMember.m_id = manager.m_id;
          // console.log(this.localMember.m_id)
        } else {
          const manager = this.ManagerData.find(manager => manager.m_name === this.name1);
          this.localMember.m_id = manager.m_id;
        }
      }, 2000);
      
    },
    // Customer
    // changingCustomerName(event){
    //   if(this.changeStatus){
    //     // console.log(this.changeStatus)
    //     this.localMember.cus_name = event.target.value;
    //   }
    // },
    changingEmail(event) {
      setTimeout(() => {
        let email1 = this.localMember.email;
        // console.log("email1 : " + email1);     

        let email2 = event.target.value;
        // console.log("email2 : " + email2);

        if (this.newStatus) {
          this.selectedEmail = email2;
          console.log('selectedEmail: ' + this.selectedEmail)
          this.localMember.email = this.selectedEmail;
          console.log('localMemberEmail: ' + this.selectedEmail)
        } else {
          this.selectedEmail = email1;
          console.log('selectedEmail: ' + this.selectedEmail)
          this.localMember.email = this.selectedEmail;
          console.log('localMemberEmail: ' + this.selectedEmail)
        }
      }, 2500);
    },
    
    changingTel(event) {
      setTimeout(() => {
        let tel1 = this.localMember.tel;
        // console.log("tel1 : " + tel1);     

        let tel2 = event.target.value;
        // console.log("tel2 : " + tel2);

        if (this.newStatus) {
          this.selectedTel = tel2;
          // console.log('selectedTel: ' + this.selectedTel)
          this.localMember.tel = this.selectedTel;
          // console.log('localMemberTel: ' + this.selectedTel)
        } else {
          this.selectedTel = tel1;
          // console.log('selectedTel: ' + this.selectedTel)
          this.localMember.tel = this.selectedTel;
          // console.log('localMemberTel: ' + this.selectedTel)
        }
      }, 2500);
    },
    changingPhone(event) {
      setTimeout(() => {
        let phone1 = this.localMember.phone;
        // console.log("phone1 : " + phone1);     

        let phone2 = event.target.value;
        // console.log("phone2 : " + phone2);

        if (this.newStatus) {
          this.selectedPhone = phone2;
          // console.log('selectedPhone: ' + this.selectedPhone)
          this.localMember.phone = this.selectedPhone;
          // console.log('localMemberPhone: ' + this.selectedEmail)
        } else {
          this.selectedPhone = phone1;
          // console.log('selectedPhone: ' + this.selectedPhone)
          this.localMember.phone = this.selectedPhone;
          // console.log('localMemberPhone: ' + this.selectedPhone)
        }
      }, 2500);
    },
    changingJob(event) {
      setTimeout(() => {
        let job1 = this.localMember.job;
        // console.log("job1 : " + job1);     

        let job2 = event.target.value;
        // console.log("job2 : " + job2);

        if (this.newStatus) {
          this.selectedJob = job2;
          // console.log('selectedTel: ' + this.selectedEmail)
          this.localMember.job = this.selectedJob;
          // console.log('localMemberEmail: ' + this.selectedEmail)
        } else {
          this.selectedJob = job1;
          // console.log('selectedTel: ' + this.selectedTel)
          this.localMember.job = this.selectedJob;
          // console.log('localMemberTel: ' + this.selectedTel)
        }
      }, 2500);
    }, 
    
    changingAddr(event) {
      setTimeout(() => {
        let addr1 = this.localMember.addr;
        // console.log("addr1 : " + addr1);     

        let addr2 = event.target.value;
        // console.log("addr2 : " + addr2);

        if (this.newStatus) {
          this.selectedAddr = addr2;
          // console.log('selectedAddr: ' + this.selectedEmail)
          this.localMember.addr = this.selectedAddr;
        } else {
          this.selectedAddr = addr1;
          // console.log('selectedAddr: ' + this.selectedTel)
          this.localMember.addr = this.selectedAddr;
        }
      }, 10000);
    },   

  }
 


};
</script>

<style>

</style>
