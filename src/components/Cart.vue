<template>
    <div class="cart">
        <OpenModal :isOpen="isOpenModal" @close-modal="isCloseModal"/>
        <div class="cart-list">
            <h2>장바구니</h2>
            <h4 v-if="cart.length === 0">장바구니가 비었습니다</h4>
            <ul v-else>
                <li v-for="list in cart" :key="list.id">
                    <img :src="list.image" :alt="list.name">
                    <p>{{ list.name }}</p>
                    <p>가격 : {{ list.price }}</p>
                    <p>수량 : {{ list.count }}</p>
                    <button @click="removeCart(list.id)">X</button>
                </li>
            </ul>
        </div>
        <div class="cart-add">
            <h2>주문내역</h2>
            <div class="total">
                <p>상품금액 : {{ totalPrice }}</p>
                <p>배송비 : {{ shippingFee === 0 ? '무료' : `${shippingFee}원` }}</p>
                <p>(배송비 3,000원 5만원 이상 구매시 무료배송)</p>
                <p>총 결제금액 : {{ `${payment}원` }}</p>
                <button @click="handleOpen">주문결제</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import OpenModal from './OpenModal.vue';
import { useRouter } from 'vue-router';

    const isOpenModal = ref(false);

    //라우터 인스턴스 생성
    const router = useRouter();

    //모달창 열림
    const handleOpen = () => {
        isOpenModal.value = true;
    }
    //모달창 닫힘
    const isCloseModal = (value) => {
        isOpenModal.value = value;
        emit('clear-cart',true);
        router.push('/'); //상품 목록 페이지로 이동
    }
    const props = defineProps({
        cart: Array
    });
    const emit = defineEmits(['remove-cart-id', 'clear-cart']);
    const removeCart = (cartID) => {
        emit('remove-cart-id',cartID);
    }

    //상품금액
    const totalPrice = computed(()=>{
        // let sum = 0;
        // props.cart.forEach((item)=>{
        //     //가격 * 수량
        //     sum += item.price * item.count;
        // });
        // return sum;

        //배열 객체 사용
        let result = props.cart.reduce((sum,item)=>{
            return sum += item.price * item.count
        },0);
        return result;
    });
    //배송비
    const shippingFee = computed(()=>{
        return totalPrice.value >= 50000 ? 0 : 3000;
    });
    //총 결제금액
    const payment = computed(()=>{
        return totalPrice.value + shippingFee.value;
    });
</script>

<style lang="scss" scoped>
    .cart{
        padding: 2rem 5rem;
        display: flex;
        gap: 5rem;
        div{
            padding: 1rem;
            flex: 1;
            border-radius: 5px;
            border: 1px solid #222;
        }
        .cart-list{
            h2{
                padding: 10px 0;
            }
            h4{
                    font-weight: lighter;
            }
            ul{
                li{
                    padding: 1rem;
                    padding-bottom: 1rem;
                    display: flex;
                    align-items: center;
                    gap: 1rem;
                    img{
                        width: 100px;
                        height: 100px;
                    }
                }
            }
        }
        .cart-add{
            .total{
                padding: 1rem;
                border: none;
                p{
                    padding: 10px 0;
                }
                button{
                    width: 100px;
                    padding: 3px 0;
                    outline: none;
                }
            }
        }
    }
</style>