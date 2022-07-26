<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width: 100%">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <input v-model = "month">
      <p> {{ month }}개월 선택함 : {{ 원룸들[누른거].price * month}}원</p>
      <button @click="close">닫기</button>
    </div>
  </div>
</template>


<script>
export default {
  name : "Modal_",
  data() {
    return {
      month : 1,
    }
  },
  watch : {
    month(a) {
      if (a >= 13) {
        alert('13이상 입력 ㄴㄴ');
        this.month = 1;
      }
      if (isNaN(a) == true) {
        alert('문자입력 ㄴㄴ');
        this.month = 1;
      }
    }
  },
  props : {
    원룸들 : Array,
    누른거 : Number,
    모달창열렸니 : Boolean,
  },
  beforeUpdate(){
    if (this.month == 2){
      alert('2개월은 너무 적다');
      this.month = 3;
    }
  },
  methods: {
    close() {
      this.$emit('closeModal')
    }
  },
}
</script>

<style>

</style>