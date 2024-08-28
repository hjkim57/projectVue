<template>
  <!-- As a heading -->
    <div class="header">
      <ul class="header-title">
        <li>고객정보관리</li>
      </ul>
      <ul class="header-button">
        <button class="btn-close" id="b-close">x</button>
      </ul>
    </div>
  
    <div class="container-wrap">
      <!-- <div class="container1">
        <div class="inform"><b>고객성명 : </b></div>
        <input type="text" id="search_name"><br>
        <button id="filter">조건 검색</button><br>
        <button id="all">전체 검색</button>
        <fieldset class="names">
          <input type="radio">
          <input type="radio" name="customers" checked>윤OO<br>
          <input type="radio" name="customers">강해라<br>
          <input type="radio" name="customers">나란다<br>
          <input type="radio" name="customers">라면다<br>
          <input type="radio" name="customers">박석일<br>
          <input type="radio" name="customers">이성경
        </fieldset>
      </div> -->
  
      <!-- <div class="container2">
        <ul class="information">
          <label for="c_date">**작성일자:</label>
          <input type="date" id="c_date"> 
          <br>
          <label for="c_name">*고객명:</label>
          <input type="text" id="c_name" > 
          <br>
          <label for="c_jm_number">*실명번호:</label>
          <input type="number" id="c_jm_number" > 
          <br>
          <label for="c_email">*E-mail:</label>
          <input type="email" id="c_email" > 
          <br>
          <label for="c_home_call">전화번호:</label>
          <input type="text" id="c_home_call" > 
          <br>
          <label for="c_phone_call">*핸드폰 번호:</label>
          <input type="text" id="c_phone_call" > 
          <br>
          <label for="job">*직업:</label>
          <input type="text" id="job" > 
          <br>
          <label for="c_address">주소:</label>
          <input type="text" id="c_address" > 
          <br>
          <hr>
          <br>
          <label for="m_name">관리담당자:</label>
          <select id="m_name">
            <option value="강하게">강하게</option>
            <option value="나대리">나대리</option>
            <option value="고과장">고과장</option>
          </select>
          <br>
          <label for="dept">**부서:</label>
          <input type="text" id="dept" > 
          <br>
          <label for="position">**직위:</label>
          <input type="text" id="position" > 
          <br>
          <label for="m_phone">**연락처:</label>
          <input type="text" id="m_phone" > 
        </ul>
      </div> -->
  
      <!-- <div class="container3">
        <div class="counseling"><b>상담내역 : </b></div>
        <fieldset class="counsel">
          <ul>
            <li>상담1</li>
            <li>상담2</li>
            <li>상담3</li>
          </ul>
        </fieldset>
        <div id="buttons">
          <div id="buttons_up">
            <input class="buttons" type="button" id="register" value="등록">
            <input class="buttons" type="button" id="modify" value="변경">
            <input class="buttons" type="button" id="delete" value="삭제">
            <input class="buttons" type="button" id="new" value="신규">
          </div>
          <div id="buttons_down">  
            <input class="buttons_exc" type="button" id="search" value="고객조회">
            <input class="buttons" type="button" id="quit" value="종료">
          </div>
        </div>
      </div>   -->
      <CustomerVue></CustomerVue>
      <!-- <InformationVue></InformationVue> -->
      <!-- <CounselVue></CounselVue> -->
      <!-- <transition name="modal">
        <ModalVue @CloseModal="modalStatus=false" :modalStatus="modalStatus" />
      </transition> -->
    </div>
  
    <ModalVue />
    
  
  </template>
  
  <script>
  
  import CustomerData from './assets/customer.js';
  import CustomerVue from './components/Customer.vue';
  import ModalVue from './components/Modal.vue';
  // import InformationVue from './components/Information.vue';
  // import CounselVue from './components/Counsel.vue';
  
  export default {
    name: 'App',
    data() {
      return {
        CustomerData : CustomerData,
  
      }
    },
    components: {
      CustomerVue,
      ModalVue,
      // InformationVue,
      // CounselVue,
    },
  }
  </script>
  
  <style>
  
  @import './assets/css/app.css';
  
  </style>
  