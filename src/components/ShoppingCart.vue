<template>
    <div>
        <div class="cart">
            <div class="cart__header">
                <h2>Корзина</h2>
                <div class="cart__info">
                    <div class="cart__goods">
                        {{ getCount }} товаров
                    </div>
                    <div class="cart__sum">
                        Сумма: {{ getSum }} (gross), {{ getNetPrice }} (net)
                    </div>
                </div>
            </div>
            <ul class="list">
                <li v-for="(item, index) in cart" :key="item.id" class="list__item">
                    <div class="item__index"> {{ index + 1 }} </div>
                    <div class="item__name"> {{ item.name }} </div>
                    <div class="item__price"> Цена (1 шт): {{ item.price }} </div>
                    <div class="item__count"> Кол-во: {{ item.count }} </div>  
                    <div class="item__cost"> Стоимость: {{ item.count * item.price }} </div> 
                    <button class="list__button" @click="deleteCard(index)">Удалить</button>    
                </li>
            </ul>
        </div>
      
    </div>
</template>

<script>
    export default {
        name: 'ShoppingCart',
        props: ['cart'],
        computed: {
            getCount() {
                return this.cart.reduce((acc, curr) => acc + curr.count, 0)
            },
            getSum() {
                return this.cart.reduce((acc, curr) => acc + curr.price * curr.count, 0)
            },
            getNetPrice() {
                return this.getSum*87/100;
            },
        },
        methods: {
            deleteCard(index) {
                this.$emit('deleteFromCart', index);
            }
        }
    }
</script>

<style scoped>
h2 {
    font-size: 28px;
}
.cart {
    margin: 0 auto;
    width: 960px;
}
.cart__header {
    display: flex;
    flex-direction: column;
}
.cart__goods, .cart__header {
    font-size: 20px;
}
.list {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 0;
}
.list__item {
    list-style-type: none;
    display: flex;
    justify-content: space-around;
    padding: 15px 30px;
    border-radius: 4px;
    line-height: 2;
    background: #D5DCE5;
}

.list__button {
    padding: 10px 12px;
    cursor: pointer;
    background: #7CABE3;
    color: #FFFFFF;
    border: none; 
    border-radius: 4px;

    font-weight: 400;
    font-size: 16px;
    line-height: 16px;
}
</style>