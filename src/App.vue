<template>

  <div>
    <div class="black-bg" v-if="isModalOpen==true">
      <div class="white-bg">
        <h4>Details</h4>
        <p>Detail contents</p>
        <button @click="isModalOpen=false">close</button>
      </div>
    </div>
    <div class="menu">
      <a v-for="(menu, idx) in menus" :key="idx">{{menu}}</a>
    </div>
    <div v-for="product in products" :key="product">
      <img :src="product.image" class="room-img"/>
      <h4 @click="isModalOpen=true">{{product.title}}</h4>
      <p>{{product.price}}원</p>
      <button @click="addCount(product)">허위 매물 신고</button> <span>신고수 : {{product.count}}</span>
    </div>

  </div>
</template>

<script>
import products from './assets/post.js'

export default {
  name: 'App',
  data() {
    return {
      menus: [`Home`, `Products`, `About`],
      products : products,
      isModalOpen: false,
    }
  },
  methods : {
    addCount(product) {
      product.count+=1;
    }
  },
  components: {
  }
}
</script>

<style>
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

.room-img {
  width: 100%;
  margin-top: 40px;
}

body {
  margin : 0;
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

</style>
