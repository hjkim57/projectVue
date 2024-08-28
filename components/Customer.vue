<template>
  <div class="container1">
      <div class="inform"><b>고객성명 : </b></div>
      <input type="text" id="search_name" v-model="findPerson"><br>
      <!-- <button id="filter">조건 검색</button><br> -->
      <input class="buttons" type="button" id="filter" @click="filtering" value="조건 검색">
      <input class="buttons" type="button" id="all" @click="allShow" value="전체 검색">
      <!-- <button id="all">전체 검색</button> -->
      <fieldset class="names">
        <label v-for="mem in copyCustomerData" :key="mem.cus_id">
        <input type="radio" name="customers" :value="mem.cus_name" v-model="myPicked" />
        {{ mem.cus_name }}<br>
      </label>
        <!-- <input type="radio" name="customers" v-for="mem in CustomerData" :key="mem" v-bind:value="mem.cus_id" v-model="myPicked">
        {{ mem.cus_name }} -->

        <!-- <input type="radio" name="customers" value="윤하나" v-model="myPicked" checked>윤하나<br>
        <input type="radio" name="customers" value="강해라" v-model="myPicked">강해라<br>
        <input type="radio" name="customers" value="나란다" v-model="myPicked">나란다<br>
        <input type="radio" name="customers" value="담나라" v-model="myPicked">담나라<br>
        <input type="radio" name="customers" value="라면다" v-model="myPicked">라면다<br>
        <input type="radio" name="customers" value="박석일" v-model="myPicked">박석일<br>
        <input type="radio" name="customers" value="이성경" v-model="myPicked">이성경<br>
        <input type="radio" name="customers" value="김임시" v-model="myPicked">김임시 -->
        <!-- <p>{{ myPicked }}</p> -->
        <!-- {{CustomerData[0]}} -->
      </fieldset>
  </div>

  <InformationVue :CustomerData="CustomerData" :myPicked="myPicked"></InformationVue>
  <CounselVue :CustomerData="CustomerData" :myPicked="myPicked" @addMember="adding"></CounselVue>

</template>

<script>

import CustomerData from '../assets/customer.js';
import InformationVue from './Information.vue';
import CounselVue from './Counsel.vue';

export default {
    name: 'CustomerVue',
    data() {
      return {
        CustomerData : CustomerData,
        myPicked:'윤하나',
        findPerson : '',
        copyCustomerData : [...CustomerData],
      }
    },
    props: {
        newmember : Object,
    },
    components : {
      InformationVue,
      CounselVue,
    },

    computed : {
      // filtering() {
      //   // Ensure CustomerData is defined and is an array
      //   if (Array.isArray(this.CustomerData)) {
      //     return this.CustomerData.find(customer => customer.cus_name === this.findPerson) || {};
      //   }
      //   return {}; // Return an empty object if CustomerData is not an array
      // },
    },

    methods : {
      // adding() {
      //   this.CustomerData.push(this.addMember)
      // },
      adding(newMember) {
        newMember.cus_id = CustomerData.length+1
        this.CustomerData.push(newMember)
        // Handle the newMember data (e.g., update data, make API calls, etc.)
      },
      filtering() {
        // Ensure CustomerData is defined and is an array
        if (Array.isArray(this.CustomerData)) {
          this.copyCustomerData = this.CustomerData.filter(customer => customer.cus_name === this.findPerson) || {};
        }
        return {}; // Return an empty object if CustomerData is not an array
      },
      allShow(){
        return this.copyCustomerData = this.CustomerData
      }
      
    }

};

</script>

<style>

</style>