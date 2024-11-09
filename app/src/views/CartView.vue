<template>
    <div>
        <div class="heading" v-if="currentLanguage == 'English'">
            <h3>shopping cart</h3>
            <p><router-link to="/">početna</router-link> <span> / cart</span></p>
        </div>
        <div class="heading" v-if="currentLanguage == 'Srpski'">
            <h3>korpa</h3>
            <p><router-link to="/">početna</router-link> <span> / korpa</span></p>
        </div>

        <section class="products">
            <h1 class="title" v-if="currentLanguage == 'English'">your cart</h1>
            <h1 class="title" v-if="currentLanguage == 'Srpski'">vaša korpa</h1>
            <div class="cart-total">
                <p v-if="currentLanguage == 'English'">grand total : <span>${{ totalPrice }}/-</span></p>
                <p v-if="currentLanguage == 'Srpski'">ukupno za plaćanje : <span>${{ totalPrice }}/-</span></p>
                <router-link to="/checkout" class="btn" v-if="currentLanguage == 'English'">checkout orders</router-link>
                <router-link to="/checkout" class="btn" v-if="currentLanguage == 'Srpski'">narudžbine za naplatu</router-link>
            </div>

            <div class="box-container">
                <div class="box" v-for="item in cartItems" :key="item.id">
                    <button class="fas fa-times" type="button" @click="confirmDeletion(item.id)"></button>
                    <img :src="item.image" :alt="item.name">
                    <div class="name">{{ item.name }}</div>
                    <div class="flex">
                        <div class="price"><span>$</span>{{ item.price }}</div>
                        <input type="number" name="qty" class="qty" min="1" max="99" v-model.number="item.quantity" @input="updateQuantity(item, $event)">
                        <button type="button" class="fas fa-edit" @click="editItem()"></button>
                    </div>
                    <div class="sub-total" v-if="currentLanguage == 'English'">sub total : <span>${{ item.price * item.quantity }}</span></div>
                    <div class="sub-total" v-if="currentLanguage == 'Srpski'">ukupno : <span>${{ item.price * item.quantity }}</span></div>
                </div>
            </div>

            <div class="more-btn">
                <button class="delete-btn" @click="confirmDeletion('all')" v-if="currentLanguage == 'English'">delete all</button>
                <button class="delete-btn" @click="confirmDeletion('all')" v-if="currentLanguage == 'Srpski'">izbaci sve</button>
            </div>
        </section>    
    </div>    
</template>

<script>
export default {
    name: 'CartView',
    data() {
        return {
            cartItems: [],
            totalPrice: 0,
            currentLanguage: 'English',
        };
    },
    created() {
        if (localStorage.getItem('cart') != null) {
            this.cartItems = JSON.parse(localStorage.getItem('cart'));
            this.calculateTotalPrice();
        }
        // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
    },
    methods: {
        calculateTotalPrice() {
            this.totalPrice = this.cartItems.reduce((total, item) => {
                return total + (item.price * item.quantity);
            }, 0);
        },
        confirmDeletion(id) {
            const message = id === 'all' ? 'delete all from cart?' : 'delete this item?';
            if (confirm(message)) {
                if (id === 'all') {
                    this.cartItems = [];
                    this.totalPrice = 0;
                } else {
                    this.cartItems = this.cartItems.filter(item => item.id !== id);
                }
                localStorage.setItem('cart', JSON.stringify(this.cartItems));
                this.calculateTotalPrice();
            }
        },
        editItem() {        //proslediti id
            localStorage.setItem('cart', JSON.stringify(this.cartItems));
        },
        updateQuantity(item, event) {
            // Ažuriramo količinu stavke
            const newQuantity = parseInt(event.target.value);
            if (!isNaN(newQuantity) && newQuantity >= 1 && newQuantity <= 99) {
                item.quantity = newQuantity;
                localStorage.setItem('cart', JSON.stringify(this.cartItems));
                this.calculateTotalPrice();
            } else {
                console.log('Invalid quantity input');
            }
        },
        limitInputLength(event) {
            if (event.target.value.length >= 2) {
                event.preventDefault();
            }
        }
    },
};
</script>
