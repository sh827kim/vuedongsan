<template>
    <div>
      <img :src="product.image" class="room-img"/>
      <h4 @click="$emit('openModal', product.id)">{{product.title}}</h4>
      <p>{{product.price}}원</p>
      <button @click="$emit('addCount')">허위 매물 신고</button> <span>신고수 : {{product.count}}</span>
    </div>

</template>
<script>
export default {
    name: `Products`,
    props: {
        product: Object,
    },
    methods: {

    }
}
</script>
<style scoped>

</style>