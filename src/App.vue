<template>
  <div>
    <!--
    <div class="start" :class="{end: isModalOpen}">
      <Modal @closeModal="isModalOpen=false" v-bind:products="products" v-bind:isModalOpen="isModalOpen" v-bind:clickedIndex="clickedIndex"/>
    </div>
    -->
    <transition name="fade">
      <Modal @closeModal="isModalOpen=false" v-bind:products="products" v-bind:isModalOpen="isModalOpen" v-bind:clickedIndex="clickedIndex"/>
    </transition>
    <div class="menu">
      <a v-for="(menu, idx) in menus" :key="idx">{{menu}}</a>
    </div>
    <Discount v-if="showDiscount" :discountPercent="discountPercent"/>
    <button @click="sortByPriceAsc">낮은 가격순</button>
    <button @click="sortByPriceDesc">높은 가격순</button>
    <button @click="sortByTitle">제목순</button>
    <button @click="sortBack">되돌리기</button>
    <Products @openModal="changeModalView(true, $event)" @addCount="addCount(idx)" v-for="(product, idx) in products" :key="idx" :product="products[idx]"/>

  </div>
</template>

<script>
import products from './assets/post.js';
import Discount from './components/Discount.vue';
import Modal from './components/Modal.vue';
import Products from './components/Products.vue';

export default {
  name: 'App',
  data() {
    return {
      menus: [`Home`, `Products`, `About`],
      products : products,
      productsOriginal: [...products],
      isModalOpen: false,
      clickedIndex : 0,
      showDiscount: true,
      discountPercent: 30,
    }
  },
  methods : {
    addCount(idx) {
      this.products[idx].count+=1;
    },
    changeModalView(isModalOpen, clicked) {
      this.isModalOpen = isModalOpen;
      this.clickedIndex = clicked;
    },
    sortByPriceAsc() {
      this.products.sort(function(a, b) {
        return a.price - b.price;
      });
    },
    sortByPriceDesc() {
      this.products.sort(function(a, b) {
        return b.price - a.price;
      })
    },
    sortByTitle() {
      this.products.sort(function(a, b) {
        let aTitle = a.title;
        let bTitle = b.title;
        if(aTitle < bTitle) return -1;
        else if(aTitle==bTitle) return 0;
        else return 1;
      });
    },
    sortBack() {
      this.products = [...this.productsOriginal];
    }
  },
  mounted() {
    setInterval(() => this.discountPercent-=1, 1000);
  },
  components: {
    Discount: Discount,
    Modal: Modal,
    Products: Products,
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

.fade-enter-from {
  opacity: 0;
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
  transform: translateY(0px);
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}


.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

</style>
