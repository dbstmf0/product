<template>
    <nav>
        <h1>맛있게먹자</h1>
        <ul>
            <li v-for="(list,idx) in categories" :key="idx" @click="selectedClick(list)">{{ list }}</li>
        </ul>
    </nav>
</template>

<script setup>
    defineProps({
        categories: Array
    });
    const emit = defineEmits(['selected']);
    const selectedClick = (list) => {
        emit('selected',list);
    }
</script>

<style lang="scss" scoped>
    nav{
        padding: 2rem 5rem;
        display: flex;
        justify-content: space-between;
        ul{
            display: flex;
            gap: 3rem;
            li{
                cursor: pointer;
                &:hover{
                    font-weight: bolder;
                    color: tomato;
                }
            }
        }
    }
</style>