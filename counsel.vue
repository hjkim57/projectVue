<template>
  
    <div class="container3">
        <div class="counseling"><b>상담내역 : </b></div>
        <fieldset class="counsel">
          <div v-for="counsel in counseling" :key="counsel">
            <p>{{ counsel.date }} {{ counsel.time }} {{ counsel.content }}</p>
            <p></p>
            <p></p>
            
          </div>

       


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
      </div>  


</template>

<script>


export default {

    name : 'CounselVue',

    props : {

        CustomerData: Array,
        myPicked: String,
        CounselData : Array,
        // localMember : Object,

    },

    components : {



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
          // Ensure CustomerData is defined and is an array
          if (Array.isArray(this.CustomerData)) {
            return this.CounselData.filter(counsel => counsel.cus_id === this.localMember.cus_id) || {};
          }
          return {}; // Return an empty object if CustomerData is not an array
        }
      },

}
</script>

<style>

</style>