<template>
  <div class="warning-wrap" v-if="warnStatus==true">
  <div class="warn-container">
    <img src="../assets/WarningIcon.gif">
    <div v-if="step==2" class="modify">[변경] 버튼을 클릭하면 해당 고객정보가 삭제됩니다. 변경 시 복구가 불가능하므로 주의해야 합니다.</div>
    <div v-if="step==3" class="delete">[삭제] 버튼을 클릭하면 해당 고객정보가 삭제됩니다. 삭제 시 복구가 불가능하므로 주의해야 합니다.</div>
    
    <div class="modal-btn">
      <!-- <button @click="modalOpen">닫기</button> -->
      <button v-if="step==2" @click="okay_modify">확인</button>
      <button v-if="step==3" @click="okay_delete">확인</button>
      <button v-if="step==2" @click.stop="" @click="no">취소</button>
      <button v-if="step==3" @click.stop="" @click="no">취소</button>
    </div>
  </div>
  </div>
</template>

<script>
export default {
    name : 'WarningVue',
    data() {
        return {
            // warnStatus: false,
            changeStatus : false,
            deleteStatus : false,
        }
    },
    
    props : {
        warnStatus : Boolean,
        step : Number,
 
    },
    methods: {
      okay_modify(){
        this.$emit('CloseWarn')
        this.changeStatus = true;
        this.$emit('change', this.changeStatus);
        // 편집 모드에서 완료 버튼을 클릭했을 때의 동작
        // this.$emit('CloseWarn');
        // this.$emit('edit', { status: this.changeStatus });
      },
      okay_delete(){
          this.$emit('CloseWarn')
          this.deleteStatus = true;
          this.$emit('delete', this.deleteStatus);
      },
      no(){
          // this.$emit('newMember',this.newMember;
          this.$emit('CloseWarn')
          this.changeStatus = false;
          this.deleteStatus = false;
          this.$emit('change', this.changeStatus);
          this.$emit('delete', this.deleteStatus);
      }
    },
}
</script>

<style>
.warning-wrap {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
}
/* modal or popup */
.warn-container {
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 550px;
  background: #fff;
  border-radius: 10px;
  padding: 30px;
  box-sizing: border-box;
  padding-top:20px
}

button {
    padding: 10px 20px;  /* 위/아래 10px, 좌/우 20px */
    margin-top:20px;
    margin-right: 10px;
    margin-left: 110px;
    font-size: 16px;     /* 글자 크기 */
    border: 1px solid #ccc; /* 테두리 색상과 두께 */
    border-radius: 5px; /* 버튼 모서리 둥글기 */
    background-color: #f0f0f0; /* 버튼 배경색 */
    cursor: pointer;     /* 마우스 커서 스타일 */
    display: inline-block;
    text-align: center;
}

</style>