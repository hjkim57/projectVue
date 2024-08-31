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

  <InformationVue :copyCustomerData="copyCustomerData" :myPicked="myPicked" :step="step" :changeStatus="changeStatus"></InformationVue>
  <CounselVue :CustomerData="CustomerData" :myPicked="myPicked" @addMember="adding" @modifyManager="changeStatus"></CounselVue>

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

    },
};
</script>

<style>

</style>
