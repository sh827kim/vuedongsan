<template>
    <div class="black-bg" v-if="isModalOpen">
      <div class="white-bg">
        <img :src="products[clickedIndex].image" class="room-img"/>
        <h4>{{products[clickedIndex].title}}</h4>
        <p>{{products[clickedIndex].content}}</p>
      <!--  <input @input="month = $event.target.value">-->
        <input v-model.number="month">
      <!--  <textarea v-model="month"></textarea>
        <select v-model="month">
           <option>234</option>
           <option>333</option>
        </select>-->
        <p>{{month}} 개월 : {{products[clickedIndex].price * month}} 원</p>
        <button @click="close">close</button>
      </div>
    </div>
</template>
<script>
export default {
    name: `Modal`,
    props: {
        products : Array,
        isModalOpen: Boolean,
        clickedIndex: Number,
    }, 
    data() {
      return {
        month: 3,
      }
    },
    watch: {
      month(a, b) { // a는 변경 전 b 는 변경 후
        if(isNaN(a) || isNaN(b)) {
          alert('문자열은 안됨.');
          this.month = 3;
        }
      },
    },
    beforeUpdate() {
      if(this.month < 3) {
        alert(`3개월부터 선택 가능합니다.`);
        this.month = 3;
      }
    },
    methods: {
      close() {
        this.$emit('closeModal');
      },
    }
}
</script>
<style scoped>

</style>
