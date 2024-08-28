<template>
  <div class="container3">
      <div class="counseling"><b>상담내역 : </b></div>
      <fieldset class="counsel">
        <div v-for="(counsel, index) in counseling" :key="index">
        <p>{{ counsel.date }} {{ counsel.time }} {{ counsel.content }}</p>
        </div>
      </fieldset>
      <div id="buttons">
        <div id="buttons_up">
          <input class="buttons" type="button" id="register" v-on:click="submitRegister" value="등록">
          <input class="buttons" type="button" id="modify" v-on:click="warning" value="변경">
          <input class="buttons" type="button" id="delete" value="삭제">
          <input class="buttons" type="button" id="new" v-on:click="modalStatus=true" value="신규">
        </div>
        <div id="buttons_down">  
          <input class="buttons_exc" type="button" id="search" value="고객조회">
          <input class="buttons" type="button" id="quit" value="종료">
        </div>
      </div>
    </div>
    
    <transition name="modal">
      <ModalVue v-if="modalStatus" @CloseModal="modalStatus=false" @newMember="handleNewMember" :modalStatus="modalStatus" />
      <!-- @CloseModal="modalStatus=false" :modalStatus="modalStatus" @newMember="handleNewMember"/> -->
    </transition>

    <transition name="warn">
      <WarningVue v-if="warnStatus" @CloseWarn="warnStatus=false" :warnStatus="warnStatus" :step="step" /> 
    </transition>

</template>

<script>

import CounselData from '../assets/counsel.js';
import ModalVue from '../components/Modal.vue';
import WarningVue from './Warning.vue';

export default {
    name :'CounselVue',
    data() {
      return {
        CounselData,
        modalStatus : false,
        addMember: {},
        warnStatus : false,
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
          return this.CustomerData.find(customer => customer.cus_name === this.myPicked) || {};
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
    },

    methods: {
      // openModal() {
      //   // 'open-modal' 이벤트를 부모 컴포넌트로 emit
      //   this.$emit('open-modal');
      // },
      // handleRegister(){
      //   console.log(this.newMember)
      //   this.$emit('newMember',this.newMember)
      //   this.$emit('CloseModal')
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
        // Optionally, you can add logic here to process the newMember data, such as sending it to a server
      },
      modifying() {
        this.warnStatus = true;
        this.step = 2;
      },
      deleting() {
        this.warnStatus = true;
        this.step = 3;
      }
      
  }

}
</script>

<style>

</style>