<template>
    <div class="product-list">
        <div class="card" v-for="list in products" :key="list.id">
            <img :src="list.image" :alt="list.name">
            <p>{{ list.name }}</p>
            <p>가격 : {{ list.price }}</p>
            <button @click="addToList(list)">장바구니 추가</button>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        products: Array
    });
    const emit = defineEmits(['add-to-cart']);
    const addToList = (list) => {
        emit('add-to-cart',list);
    }
</script>

<style lang="scss" scoped>
    .product-list{
        display: flex;
        justify-content: center;
        gap: 2rem;
        .card{
            width: 200px;
            text-align: center;
            img{
                width: 100%;
                height: 200px;
                border-radius: 5px;
                object-fit: cover;
            }
            p{
                padding: 5px 0;
            }
        }
    }
</style>