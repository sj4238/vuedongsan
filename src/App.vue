<template>

  <translation name="fade">
    <Modal @closeModal="모달창열렸니 = false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
  </translation>

  <div class="menu">
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
  </div>

  <Discount v-if="showDiscount == true"/>
  <p>지금 결제하면 {{amount}}% 할인</p>

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="a" />
  
</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue'

export default {
  name: 'App',
  data(){
    return {
      amount : 30,
      showDiscount: true,
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],     
      메뉴들 : ['Home','Shop','About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase() {
      this.신고수 ++;
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    }, 
    priceSort() {
      this.원룸들.sort(function(a, b) {
          return a.price - b.price       
      });
    },
  },

  // 1초마다 1%씩 감소
  mounted(){
    setInterval(()=>{
      if(this.amount>0){
        this.amount--;
      }
    }, 1000);
  },


  // 2초 후 Discount 컴포넌트 사라지게 하기
  // mounted() { 
  //   setTimeout(()=>{
  //     this.showDiscount = false;
  //   }, 2000);
  // },

  components: {
    Discount,
    Modal,
    Card,
  }
}
</script>

<style>
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}

body {
  margin: 0
}
div {
  box-sizing: border-box;
}
.discount {
  background: #eee ;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg {
  width: 100%; height: 100%;
  background-color: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background-color: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
