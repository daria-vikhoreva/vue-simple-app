<template>
    <div class="card">
        <div class="card__title">
            {{ card.name }}
        </div>
        <div class="card__info">
            <div class="price__gross">
                Цена (gross) - {{ card.price }}
            </div>
            <div class="price__net">
                Цена (net) - {{ getNetPrice }}
            </div>
        </div>
        <button @click="clickButton" class="card__button">В корзину</button>
    </div>
</template>

<script>
export default {
    name: 'CardItem',
    props: ['card'],
    data() {
        return { 
            count: 0, 
        }
    },
    computed: {
        getNetPrice() {
            return this.card.price*87/100;
        }
    },
    methods: {
        clickButton() {
            this.$emit('addToCart', this.card)
        }
    },
}
</script>

<style scoped>
.card {
    border: none;
    /* border-radius: 10px; */
    background: #FFFFFF;
    border-radius: 4px;
    /* background-color:gainsboro; */
    padding: 30px 30px;
    margin: 15px 20px;
    width: 200px;
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.card__title {
    font-weight: 500;
    font-size: 18px;
    line-height: 18px;
}

.card__info {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.card__button {
    display: block;
    max-width: max-content;
    padding: 10px 12px;
    margin: 0 auto;
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

