<template>
    <div v-if="isOpen" class="modal-overlay">
        <div class="modal">
            <h2>주문 완료</h2>
            <p>주문이 성공적으로 완료되었습니다</p>
            <button @click="handleClose">확인</button>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        isOpen: Boolean
    });
    const emit = defineEmits(['close-modal']);
    const handleClose = () => {
        emit('close-modal',false);
    }
</script>

<style lang="scss" scoped>
    .modal-overlay{
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(0,0,0,0.8);
        border: none;
        .modal{
            padding: 3rem 5rem;
            background-color: #fff;
            border-radius: 5px;
        }
    }
</style>