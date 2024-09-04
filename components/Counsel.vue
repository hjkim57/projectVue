<template>
  <div class="container3">
      <div class="counseling"><b>상담내역 : </b></div>
      <fieldset class="counsel">
        <div v-for="(counsel, index) in counseling" :key="index">
        <p>{{ counsel.date }} {{ counsel.time }} {{ counsel.content }}</p>
        </div>
      </fieldset>
        <div id="buttons_up">
          <input type="button" id="register" 
          value="등록" v-on:click="submitRegister" :disabled="step == 0">
          <input type="button" id="modify" v-on:click="modifying" value="변경">
          <input type="button" id="delete" v-on:click="deleting" value="삭제">
          <input @click="step = 1" type="button" id="new" v-on:click="modalStatus=true" value="신규">
        </div>
        <div id="button_search">  
          <input v-on:click="modalsearchStatus = true" type="button" id="search" value="고객조회">
        </div>  
        <div id="button_quit">
          <input @click="step = 0, modalStatus=false" type="button" id="quit" value="종료">
        </div>
    </div>
    
    <transition name="modal">
      <ModalVue v-if="modalStatus" @CloseModal="modalStatus=false" @newMember="handleNewMember" :modalStatus="modalStatus" />
    </transition>

    <transition name="warn">
      <WarningVue v-if="warnStatus" @CloseWarn="warnStatus=false" @change="handleChangeStatus" @delete="handleDeleteStatus" 
      :warnStatus="warnStatus" :step="step" /> 
    </transition>

    <Transition name="modalSearch">
      <Modal_searchVue v-if="modalsearchStatus" @CloseModalsearch="modalsearchStatus=false" @newMember="handleNewMember" :modalsearchStatus="modalsearchStatus" />
    </Transition>
    <!-- <Information /> -->

    
</template>

<script>

import CounselData from '../assets/counsel.js';
import ModalVue from './Modal.vue';
import WarningVue from './Warning.vue';
import Modal_searchVue from './modal_search.vue';
// import Modal_searchVue from './modal_search.vue';
// import Information from './Information.vue';

export default {
    name :'CounselVue',
    data() {
      return {
        CounselData,
        modalStatus : false,
        addMember: {},
        warnStatus : false,
        step : 0,
        changeStatus :false,
        modalsearchStatus : false,
      }
    },
    props : {
      CustomerData: Array,
      myPicked: String,
      newMember: Object,
    },
    computed: {
      localMember() {
        // Ensure CustomerData is defined and is an array
        if (Array.isArray(this.CustomerData)) {
          return this.CustomerData.find(customer => customer.cus_id === this.myPicked) || {};
        }
        return {}; // Return an empty object if CustomerData is not an array
      },
      counseling() {
        // Ensure CounselData is defined and is an array
        if (Array.isArray(this.CounselData) && this.localMember.cus_id) {
          return this.CounselData.filter(counsel => counsel.cus_id === this.localMember.cus_id);
        }
        return {};
      },
      
    },
    components: {
      ModalVue,
      WarningVue,
      Modal_searchVue,
      // Information,
    },

    methods: {
      // openModal() {
      //   // 'open-modal' 이벤트를 부모 컴포넌트로 emit
      //   this.$emit('open-modal');
      // },

      handleNewMember(newMember) {
        this.addMember = newMember;
        console.log(this.addMember);
        // Handle the newMember data (e.g., update data, make API calls, etc.)
      },
      submitRegister() {
        // This function can be used to handle additional logic if needed
        // For now, it just logs the newMember data
        this.$emit('addMember', this.addMember)
        console.log(this.addMember);
        this.modalStatus=false; 
        this.step = 0;
        // Optionally, you can add logic here to process the newMember data, such as sending it to a server
      },
      modifying() {
        this.warnStatus = true;
        this.step = 2;
        
      },
      deleting() {
        this.warnStatus = true;
        this.step = 3;
        this.$emit('deleteInform', this.deleteStatus)
      },
      handleChangeStatus(status) {
        this.changeStatus = status;
        // console.log('Change status:', this.changeStatus);
        this.$emit('modifyManager', this.changeStatus)
        // Handle the updated change status here
      },
      handleDeleteStatus(status) {
        this.deleteStatus = status;
        this.$emit('deleteCustomer', this.deleteStatus);
        console.log('Delete status:', this.deleteStatus);
        // Handle the updated delete status here
      },
      
  }

}
</script>

<style>

</style>