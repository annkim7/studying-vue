<template>
  <!-- <div class="start" :class="{ end : modal }">
    <Modal @closeModal="modal=false" :rooms="rooms" :number="number" :modal="modal"/>
  </div> -->

  <transition name="fade">
    <Modal @closeModal="modal=false" :rooms="rooms" :number="number" :modal="modal"/>
  </transition>
  

  <div class="menu">
    <a v-for="nav in menus" :key="nav">{{nav}}</a>
  </div>


  <Discount v-if="showDiscount == true"/>

  <button @click="priceSort">가격순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="modal=true; number=$event"  :room="rooms[i]" v-for="(a,i) in rooms" :key="a"/>

</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';


export default {
  name: 'App',
  data(){
    return {
      showDiscount: true,
      original : [...data],
      number : 0,
      rooms: data,
      modal: false,
      report: [0,0,0],
      menus : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      money : ['50 만원', '70 만원', '60 만원']
    }
  },
  methods: {
    increase(){
      this.report += 1;
    },
    sortBack(){
      this.rooms = [...this.original];
    },
    priceSort(){
      this.rooms.sort(function(a,b){
        return a.price - b.price
      });
    },
  },

  created(){
    
  },

  mounted(){
    setTimeout(()=>{
      this.showDiscount = false;
    }, 2000);
  },

  components: {
    Discount,
    Modal,
    Card,
  }
}
</script>

<style>
body{
  margin:0;
}
div{
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg{
  width:100%; height:100%;
  background: rgba(0,0,0,0.5);
  position:fixed; padding: 20px;
}
.white-bg{
  width:100%; background:white;
  border-radius: 8px;
  padding: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a{
  color: white;
  padding: 10px;
}

.room-img{
  width:100%;
  margin-top:40px;
}

.start{
  opacity:0;
  transition: all 1s;
}
.end{
  opacity:1;
}

.fade-enter-from{
  opacity:0;
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  opacity:1;
}

.fade-leave-from{
  opacity:1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity:0;
}
</style>
