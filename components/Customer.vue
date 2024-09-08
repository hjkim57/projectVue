<template>
  <div class="container1">
      <div class="inform"><b>고객성명 : </b></div>
      <input type="text" id="search_name" v-model="findPerson"><br>
      <input type="button" id="filter" @click="filtering" :disabled="findPerson.length==0" value="조건 검색">
      <input type="button" id="all" @click="allShow" value="전체 검색">
      <fieldset class="names">
        <label v-for="mem in copyCustomerData" :key="mem.cus_id">
          <input type="radio" name="customers" :value="mem.cus_id" v-model="myPicked" />
          {{ mem.cus_name }}<br>
        </label>
      </fieldset>
  </div>

  <InformationVue :copyCustomerData="copyCustomerData" :myPicked="myPicked" :step="step" 
  :changeStatus="changeStatus" :newStatus="newStatus" @nameChange="changingName" :newName="newName"></InformationVue>
  <CounselVue :CustomerData="CustomerData" :myPicked="myPicked" @addMember="adding" 
  @modifyManager="changing" @deleteCustomer="deleting"></CounselVue>

</template>

<script>
import CustomerData from '../assets/customer.js';
import InformationVue from './Information.vue';
import CounselVue from './Counsel.vue';

export default {
    name: 'CustomerVue',
    data() {
      return {
        CustomerData: CustomerData,
        myPicked: 1,
        findPerson: '',
        copyCustomerData: [...CustomerData],
        step:0,
        changeStatus : true,
        newStatus : true,
        newName : null,
        deleteStatus : false,
      }
    },
    props: {
        newmember: Object,
    },
    components: {
      InformationVue,
      CounselVue,
    },

    methods: {
      adding(newMember) {
        newMember.cus_id = this.CustomerData.length + 1;
        this.CustomerData.push(newMember);
        this.copyCustomerData.push(newMember); // Add to the filtered data too
      },
      
      filtering() {
        // Ensure CustomerData is defined and is an array
        if (Array.isArray(this.CustomerData)) {
          this.copyCustomerData = this.CustomerData.filter(customer => customer.cus_name === this.findPerson) || {};
        }
        return {}; // Return an empty object if CustomerData is not an array
      },

      allShow() {
        this.copyCustomerData = [...this.CustomerData];
      },

      changing(status){
        this.changeStatus = status;
        // console.log("changing 메소드 확인" + this.changeStatus);
        this.$nextTick(() => {
          // Ensure that the changeStatus is properly updated in the DOM
          // console.log('Change Status in Parent after nextTick:', this.changeStatus);
          this.newStatus = this.changeStatus;
          console.log(this.newStatus)
        });
      },

      deleting(status){
        this.deleteStatus = status;
        console.log("삭제 상태 : " + this.deleteStatus)
        if (this.deleteStatus) {
          let deleteIndex = this.myPicked; // Convert `myPicked` to zero-based index
          this.copyCustomerData.splice(deleteIndex-1, 1);

          // Update `myPicked` to the new default value
          if (this.copyCustomerData.length > 0) {
            for(let i=0; i<this.copyCustomerData.length; i++){
              if(this.copyCustomerData[i].cus_id > deleteIndex){
                this.copyCustomerData[i].cus_id -= 1;
              }
            }
            this.myPicked = this.copyCustomerData[0].cus_id;
          } else {
            // If no items left, clear `myPicked`
            this.myPicked = null;
          }
        }
      }
      
    },
    watch : {
      changeStatus(newValue, oldValue) {
        console.log('changeStatus has changed from', oldValue, 'to', newValue);
        this.newStatus = newValue;
        // console.log('새로운 상태 : ' + this.newStatus);
      }
    }
};
</script>

<style>

</style>
