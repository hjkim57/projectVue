<template>
  <div class="container2">
      <ul class="information">
        <label for="c_date">**작성일자:</label>
        <input type="text" id="c_date" v-model="localMember.create_date">
        <br>
        <label for="c_name">*고객명:</label>
        <input type="text" id="c_name" v-model="localMember.cus_name">
        <br>
        <label for="c_jm_number">*실명번호:</label>
        <input type="text" id="c_jm_number" v-model="localMember.jumin_id"> 
        <br>
        <label for="c_email">*E-mail:</label>
        <input type="email" id="c_email" v-model="localMember.email"> 
        <br>
        <label for="c_home_call">전화번호:</label>
        <input type="text" id="c_home_call" v-model="localMember.tel"> 
        <br>
        <label for="c_phone_call">*핸드폰 번호:</label>
        <input type="text" id="c_phone_call" v-model="localMember.phone"> 
        <br>
        <label for="job">*직업:</label>
        <input type="text" id="job" v-model="localMember.job"> 
        <br>
        <label for="c_address">주소:</label>
        <input type="text" id="c_address" v-model="localMember.addr"> 
        <br>
        
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
        <input type="text" id="m_phone" > {{ member }}
      </ul>
    </div>
</template>

<script>
export default {
    name: 'InformationVue',
    props : {
      CustomerData: Array,
      myPicked: String,
      
    },
    computed: {
      localMember() {
        // Ensure CustomerData is defined and is an array
        if (Array.isArray(this.CustomerData)) {
          return this.CustomerData.find(customer => customer.cus_name === this.myPicked) || {};
        }
        return {}; // Return an empty object if CustomerData is not an array
      }
    },
    // data() {
    //   return {
    //     localMember: this.computedMember(this.myPicked)  // Initialize localMember with the member data
    //   }
    // },

}
</script>

<style>

</style>