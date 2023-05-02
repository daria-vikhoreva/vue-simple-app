<template>
    <div>
        <div class="card-list">
            <div v-for="card of cards" :key="card.id" class="card-wrapper">
                <CardItem :card="card" @add-to-cart="addToCart"/>  
            </div>
        </div>
        <div>
            <ShoppingCart :cart="cart" @delete-from-cart="deleteFromCart"/>
        </div>
    </div>
</template>

<script>
import CardItem from './components/CardItem.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    CardItem,
    ShoppingCart,
  },
  data () {
    return {
        cards: [
            {id: 1, name: 'Товар №1', price: 100},
            {id: 2, name: 'Товар №2', price: 120},
            {id: 3, name: 'Товар №3', price: 130}
        ],
        cart: []
    }
  },
  methods: {
    addToCart(card) {
        const currentCardInCart = this.cart.find(elem => elem.id === card.id);

        if (currentCardInCart) {
            card.count = card.count + 1;
        } else {
            card.count = 1;
            this.cart.push(card);
        }
    },

    deleteFromCart(index) {
        if (this.cart[index].count > 1) {
            this.cart[index].count -= 1;
        } else {
            this.cart.splice(index, 1);
        }
    }
  }
}
</script>

<style>

@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap");

html, body {
  background-color:  #F5F5F5;
}

#app {
  font-family: 'Inter', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 18px;
  margin-top: 60px;
}

.card-wrapper {
  width: 300px;
}

.card-list {
  text-align: center;
  background-color: #D5DCE5;
  display: flex;
  gap: 20px;
  max-width: max-content;
  padding: 20px;
  margin: 0 auto;
  border-radius: 4px;
}
</style>
