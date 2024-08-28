<template>
  <div class="container1">
      <div class="inform"><b>고객성명 : </b></div>
      <input type="text" id="search_name"><br>
      <!-- <button id="filter">조건 검색</button><br> -->
      <input class="buttons" type="button" id="filter" value="조건 검색">
      <input class="buttons" type="button" id="all" value="전체 검색">
      <!-- <button id="all">전체 검색</button> -->
      <fieldset class="names">
        <input type="radio" name="customers" value="윤하나" v-model="myPicked" checked>윤하나<br>
        <input type="radio" name="customers" value="강해라" v-model="myPicked">강해라<br>
        <input type="radio" name="customers" value="나란다" v-model="myPicked">나란다<br>
        <input type="radio" name="customers" value="담나라" v-model="myPicked">담나라<br>
        <input type="radio" name="customers" value="라면다" v-model="myPicked">라면다<br>
        <input type="radio" name="customers" value="박석일" v-model="myPicked">박석일<br>
        <input type="radio" name="customers" value="이성경" v-model="myPicked">이성경<br>
        <input type="radio" name="customers" value="김임시" v-model="myPicked">김임시
        <!-- <p>{{ myPicked }}</p> -->
        <!-- {{CustomerData[0]}} -->
      </fieldset>
  </div>

  <InformationVue :CustomerData="CustomerData" :myPicked="myPicked"></InformationVue>
  <CounselVue :CustomerData="CustomerData" :myPicked="myPicked"></CounselVue>

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
      }
    },
    props: {
        // member : Object,
    },
    components : {
      InformationVue,
      CounselVue,
    },

};

</script>

<style>

</style>