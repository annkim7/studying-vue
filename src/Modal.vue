<template>
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <img :src="rooms[number].image" style="width:100%;">
      <h4>{{rooms[number].title}}</h4>
      <p>{{rooms[number].content}}</p>
      <input v-model="month">
      <p>{{ month }} 개월 선택함 : {{rooms[number].price * month}}원</p>
      <button @click="close">닫기</button>
    </div>
    
  </div>
</template>

<script>
export default {
    name : 'Modal',
    data(){
        return{
            month: 1,
        }
    },
    watch : {
        month(a){
            if(a >= 13){
                alert('13이상 숫자 입력은 불가합니다.')
                this.month = 1;
            }

            if(isNaN(a) == true){
                alert('문자입력은 불가합니다.')
                this.month = 1;
            }
        },
    },
    props : {
        rooms: Array,
        number: Number,
        modal: Boolean,
    },
    methods : {
        close(){
            this.$emit('closeModal')
        }
    }
}
</script>

<style>

</style>