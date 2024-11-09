<template>
    <div>
        <div class="heading" v-if="currentLanguage == 'English'">
            <h3>your orders</h3>
            <p><router-link to="/">home</router-link> <span> / orders</span></p>
        </div>
        <div class="heading" v-if="currentLanguage == 'Srpski'">
            <h3>Vaše narudžbine</h3>
            <p><router-link to="/">početna</router-link> <span> / narudžbine</span></p>
        </div>
        <section class="orders" v-if="currentLanguage == 'English'">
            <h1 class="title">placed orders</h1>
            <div class="box-container">
                <div v-for="(order, index) in userOrders" :key="index" class="box">
                    <p> placed on : <span>{{ order.date }}</span> </p>
                    <p> name : <span>{{ order.user.name }}</span> </p>
                    <p> number : <span>{{ order.user.phone }}</span> </p>
                    <p> email : <span>{{ order.user.mail }}</span> </p>
                    <p> address : <span>{{ order.address }}</span> </p>
                    <p> your orders : <span>{{ formatOrderItems(order.items) }}</span> </p>
                    <p> total price : <span>${{ order.totalPrice }}/-</span> </p>
                    <p> payment method : <span>{{ order.paymentMethod }}</span> </p>
                </div>
            </div>
            
        </section>
        <section class="orders" v-if="currentLanguage == 'Srpski'">
            <h1 class="title">Vaše narudžbine</h1>
            <div class="box-container" >
                <div v-for="(order, index) in userOrders" :key="index" class="box">
                    <p> naručeno : <span>{{ order.date }}</span> </p>
                    <p> ime : <span>{{ order.user.name }}</span> </p>
                    <p> telefon : <span>{{ order.user.phone }}</span> </p>
                    <p> email : <span>{{ order.user.mail }}</span> </p>
                    <p> adresa : <span>{{ order.address }}</span> </p>
                    <p> vaše narudžbine : <span>{{ formatOrderItems(order.items) }}</span> </p>
                    <p> ukupna cena : <span>${{ order.totalPrice }}/-</span> </p>
                    <p> način plaćanja : <span>{{ order.paymentMethod }}</span> </p>
                </div>
            </div>
            
        </section>
    </div>
</template>

<script>
export default {
    name: 'OrdersView',
    data() {
        return {
            userOrders: [],
            currentLanguage: 'English',
        };
    },
    created() {
        this.fetchUserOrders();
        // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
    },
    methods: {
        fetchUserOrders() {
            // Dohvati sve narudžbine iz local storage-a
            const allOrders = JSON.parse(localStorage.getItem('orders')) || [];
            
            // Filtriraj narudžbine za trenutno prijavljenog korisnika (pretpostavka: korisnik je spremljen u local storage)
            const currentUser = JSON.parse(localStorage.getItem('user'));
            if (currentUser) {
                this.userOrders = allOrders.filter(order => order.user.mail === currentUser.mail);
            }
        },
        formatOrderItems(items) {
            return items.map(item => `${item.name} (${item.quantity})`).join(' - ');
        }
    }
};
</script>

<style>
/* Dodaj bilo koje dodatne stilove ovdje */
</style>
