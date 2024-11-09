<template>
    <div>
        <div class="heading" v-if="currentLanguage == 'English'">
            <h3>checkout</h3>
            <p><router-link to="/">home</router-link> <span> / checkout</span></p>
        </div>
        <div class="heading" >
            <h3>naplata</h3>
            <p><router-link to="/">početna</router-link> <span> / naplata</span></p>
        </div>
        <section class="checkout" v-if="currentLanguage == 'Srpski'">

            <h1 class="title" v-if="currentLanguage == 'English'">order summary</h1>
            <h1 class="title" v-if="currentLanguage == 'Srpski'">vaš račun</h1>

            <form @submit.prevent="placeOrder">
                <div class="cart-items">
                    <h3 v-if="currentLanguage == 'English'">cart items</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">stavke računa</h3>
                    <template v-if="cartItems.length > 0">
                        <p v-for="item in cartItems" :key="item.id">
                            <span class="name">{{ item.name }}</span>
                            <span class="price">${{ item.price }} x {{ item.quantity }}</span>
                        </p>
                    </template>
                    <p v-else>No items in cart</p>
                    <p class="grand-total">
                        <span class="name" v-if="currentLanguage == 'English'" >grand total :</span>
                        <span class="name" v-if="currentLanguage == 'Srpski'">ukupna cena :</span>
                        <span class="price">${{ totalPrice }}</span>
                    </p>
                    <router-link to="/cart" class="btn" v-if="currentLanguage == 'English'">view cart</router-link>
                    <router-link to="/cart" class="btn" v-if="currentLanguage == 'Srpski'">pogledaj korpu</router-link>
                </div>
                <div class="user-info">
                    <h3 v-if="currentLanguage == 'English'">your info</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">vaše informacije</h3>
                    <p><i class="fas fa-user"></i> <span>{{this.username}}</span></p>
                    <p><i class="fas fa-phone"></i> <span>{{this.phone}}</span></p>
                    <p><i class="fas fa-envelope"></i> <span>{{this.mail}}</span></p>
                    <!-- <a href="update_profile.html" class="btn">update info</a> -->
                    <h3  v-if="currentLanguage == 'English'">delivery address</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">adresa dostave</h3>
                    <textarea v-model="address" class="box" placeholder="Enter your address here" required v-if="currentLanguage == 'English'"></textarea>
                    <textarea v-model="address" class="box" placeholder="Unesite Vašu adresu ovde" required v-if="currentLanguage == 'Srpski'"></textarea>
                    <select name="method" class="box" v-model="paymentMethod" required v-if="currentLanguage == 'English'">
                        <option value="" disabled selected>select payment method</option>
                        <option value="cash on delivery">cash on delivery</option>
                        <option value="credit card">credit card</option>
                        <option value="paypal">paypal</option>
                    </select>
                    <select name="method" class="box" v-model="paymentMethod" required v-if="currentLanguage == 'Srpski'">
                        <option value="" disabled selected>izaberite način plaćanja</option>
                        <option value="cash on delivery">plaćanje gotovinom</option>
                        <option value="credit card">creditnom karticom</option>
                        <option value="paypal">paypal</option>
                    </select>
                </div>
                <input type="submit" value="place order" name="order" class="btn order-btn">
            </form>

        </section>
    </div>
</template>

<script>
export default {
    name: 'CheckOutView',
    data() {
        return {
            cartItems: [],
            totalPrice: 0,
            address: '',
            paymentMethod: '',
            user: '',
            username: '',
            phone: '',
            mail: '',
            currentLanguage: 'English',
        };
    },
    created() {
        if (localStorage.getItem('cart') != null) {
            this.cartItems = JSON.parse(localStorage.getItem('cart'));
            this.calculateTotalPrice();
        }
        if (localStorage.getItem('address') != null) {
            this.address = localStorage.getItem('address');
        }
        if (localStorage.getItem('paymentMethod') != null) {
            this.paymentMethod = localStorage.getItem('paymentMethod');
        }
        if (localStorage.getItem('user') == null) {
            this.username = 'Not logged in';
        } else {
            this.user = JSON.parse(localStorage.getItem('user'));
            this.username = this.user.name;
            this.phone = this.user.phone;
            this.mail = this.user.mail;
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
        placeOrder() {
            if (this.user == '') {
                alert('You are not logged in');
                this.$router.push('/login');
                return;
            }
            if (this.totalPrice == 0) {
                alert('No empty orders in this restaurant');
                return;
            }
            const order = {
                user: {
                    name: this.username, 
                    phone: this.phone,
                    mail: this.mail,
                },
                address: this.address,
                paymentMethod: this.paymentMethod,
                items: this.cartItems,
                totalPrice: this.totalPrice,
                date: new Date().toISOString() // Adding date to the order
            };

            let orders = [];
            if (localStorage.getItem('orders') != null) {
                orders = JSON.parse(localStorage.getItem('orders'));
            }
            orders.push(order);
            localStorage.setItem('orders', JSON.stringify(orders));

            // Clear the cart and other order-related data
            localStorage.removeItem('cart');
            this.cartItems = [];
            this.totalPrice = 0;
            this.address = '';
            this.paymentMethod = '';

            // Optionally, navigate to an order confirmation page or display a message
            alert('Order placed successfully!');
        }
    }
};
</script>

<style>
/* Add any additional styles here */
</style>
