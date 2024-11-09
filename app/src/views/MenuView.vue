<template>
  <div>
    <div class="heading" v-if="currentLanguage == 'English'">
      <h3>our menu</h3>
      <p><router-link to="/" >home</router-link> <span> / menu</span></p>
    </div>
    <div class="heading" v-if="currentLanguage == 'Srpski'">
      <h3>naš meni</h3>
      <p><router-link to="/">početna</router-link> <span> / meni</span></p>
    </div>

    <section class="category">
      <h1 class="title search-form" style="text-decoration:none;">
        <i class="fas fa-search" style="display:inline;" @click="toggleSearch"></i>            
        <Transition>
          <form style="display:inline; margin-left:20px" v-if="showSearch">
            <input type="text" class="box" name="search_box" placeholder="search here..." maxlength="20" v-model="nameFilter"  v-if="currentLanguage == 'English'">
            <input type="text" class="box" name="search_box" placeholder="pretraži..." maxlength="20" v-model="nameFilter" v-if="currentLanguage == 'Srpski'">
          </form>
        </Transition>
        <div class="button-container" v-if="currentLanguage == 'English'">
          <button @click="sortBy('name')" class="btn">Sort by Name</button>
          <button @click="sortBy('price')" class="btn">Sort by Price</button>
          <button @click="resetSort" class="btn">Reset Sort</button>
        </div>
        <div class="button-container" v-if="currentLanguage == 'Srpski'">
          <button @click="sortBy('name')" class="btn">Sortiraj po imenu</button>
          <button @click="sortBy('price')" class="btn">Sortiraj po ceni</button>
          <button @click="resetSort" class="btn">Resetuj sortiranje</button>
        </div>
      </h1>

      <div class="box-container">
        <span class="box" @click="filter('appetizer')" :style="category == 'appetizer' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-1.png" alt="Page1">
          <h3 v-if="currentLanguage == 'English'">appetizer</h3>
          <h3 v-if="currentLanguage == 'Srpski'">predjela</h3>
        </span>
        <span class="box" @click="filter('main-dish')" :style="category == 'main-dish' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-2.png" alt="Page2">
          <h3 v-if="currentLanguage == 'English'">main-dish</h3>
          <h3 v-if="currentLanguage == 'Srpski'">glavna jela</h3>
        </span>
        <span class="box" @click="filter('dessert')" :style="category == 'dessert' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-3.png" alt="Page3">
          <h3 v-if="currentLanguage == 'English'">desserts</h3>
          <h3 v-if="currentLanguage == 'Srpski'">dezerti</h3>
        </span>
      </div>
    </section>

    <section class="products">
      <div class="box-container">
        <form class="box" v-for="item in items" :key="item.id">
          <button class="fas fa-eye" type="button" @click="showQuickView(item)"></button>
          <button class="fas fa-shopping-cart" type="button" @click="addToCart(item)"></button>
          <img :src="require(`@/assets/${item.img}`)">
          <p class="cat" @click="filter(item.category)" v-if="currentLanguage == 'English'">{{item.category}}</p>
          <p class="cat" @click="filter(item.category)" v-if="currentLanguage == 'Srpski'">{{item.categorysrb}}</p>
          <div class="name" v-if="currentLanguage == 'English'">{{item.name}}</div>
          <div class="name" v-if="currentLanguage == 'Srpski'">{{item.namesrb}}</div>
          <div class="flex">
            <div class="price">
              <span>$</span>{{item.size === 'small' ? item.price / 2 : item.price}}
            </div>
            <span class="portion-size">
              <label :for="'large-' + item.id" class="size-label">
                <span class="cat" v-if="currentLanguage == 'English'">large</span>
                <span class="cat" v-if="currentLanguage == 'Srpski'">veliko</span>
              </label>
              <input :id="'large-' + item.id" type="radio" name="size" class="size-radio" @change="selectSize(item, 'large')">
              
              <label :for="'small-' + item.id" class="size-label">
                <span class="cat" v-if="currentLanguage == 'English'">small</span>
                <span class="cat" v-if="currentLanguage == 'Srpski'">malo</span>
              </label>
              <input :id="'small-' + item.id" type="radio" name="size" class="size-radio" @change="selectSize(item, 'small')">
            </span>
            <input type="number" name="qty" class="qty" min="1" max="99" v-model="item.quantity" @keypress="handleKeypress">
          </div>
        </form>
      </div>
    </section>

    <section>
      <h1 v-if="currentLanguage == 'English'">Download PDF</h1>
      <h1 v-if="currentLanguage == 'Srpski'">Skini PDF</h1>
      <a :href="pdfUrl" download="MENU_PDF_VERSION.pdf" class="btn" v-if="currentLanguage == 'English'">
        Download Sample PDF
      </a>
      <a :href="pdfUrl" download="MENU_PDF_VERSION.pdf" class="btn" v-if="currentLanguage == 'Srpski'">
        Skini PDF primerak
      </a>
    </section>
    

    <DishView 
      v-if="showModal"
      :visible="showModal" 
      :dishImage="modalImage" 
      :dishName="modalName"
      :dishIngredients="modalIngredients"
      :dishId="modalId"
      @close="showModal = false"
    ></DishView>
  </div>
</template>

<script>
import DishView from '../components/DishView.vue';
import pdfFile from '../assets/MENU_PDF_VERSION.pdf';

export default {
  name: 'MenuView',
  components: { DishView },
  data() {
    return {
      pdfUrl: pdfFile,
      category: 'All',
      menuItems: [],
      filteredItems: [],
      activeBorder: "6px solid black",
      nameFilter: '',
      showSearch: false,
      showModal: false,
      modalImage: '',
      modalName: '',
      modalIngredients: '',
      modalId: '',
      currentLanguage: 'English',
      originalItems: [] // To store original unsorted items
    };
  },
  created() {
    this.menuItems = JSON.parse(localStorage.getItem('menu'));
    this.originalItems = this.menuItems.map(item => ({
      ...item,
      size: 'large', // Default size
      quantity: 1 // Default quantity
    }));
    this.filteredItems = this.originalItems;
    // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
  },
  methods: {
    filter(category) {
      if (this.category === category) {
        this.filteredItems = [...this.originalItems]; // Reset to original unsorted items
        this.category = 'All';
      } else {
        this.filteredItems = this.originalItems.filter(item => item.category === category);
        this.category = category;
      }
    },
    toggleSearch() {
      this.showSearch = !this.showSearch;
      if (!this.showSearch) {
        this.nameFilter = ''; // Clear search input when hiding the search form
      }
    },
    showQuickView(item) {
      this.modalImage = require(`@/assets/${item.img}`);
      if (this.currentLanguage == 'Srpski') {
        this.modalName = item.namesrb;
      } else {
        this.modalName = item.name;
      }
      if (this.currentLanguage == 'Srpski') {
        this.modalIngredients = item.ingredients;
      } else {
        this.modalIngredients = item.ingredientssrb;
      }
      this.modalId = item.id;
      this.showModal = true;
    }, 
    sortBy(key) {
      this.filteredItems.sort((a, b) => {
        if (key === 'name') {
          return a.name.localeCompare(b.name);
        } else if (key === 'price') {
          return a.price - b.price;
        }
        return 0;
      });
    },
    resetSort() {
      this.filteredItems = [...this.originalItems]; // Reset to original unsorted items
      this.category = 'All'; // Reset category filter
      this.nameFilter = ''; // Clear search filter
    },
    selectSize(item, size) {
      item.size = size;
    },
    handleKeypress(event) {
      if (event.target.value.length === 2) {
        event.preventDefault(); // Prevent entering more than 2 characters
      }
    },
    addToCart(item) {
      // Check if item already exists in cart
      const existingCartItem = this.findCartItemById(item.id);

      if (existingCartItem) {
        // Item already exists, increment quantity
        existingCartItem.quantity += item.quantity;
      } else {
        // Item does not exist, add to cart
        const cartItem = {
          id: item.id,
          name: item.name,
          image: item.img,
          size: item.size,
          quantity: item.quantity,
          ingredients: item.ingredients,
          price: item.size === 'small' ? item.price / 2 : item.price
        };
        
        const currentCart = JSON.parse(localStorage.getItem('cart')) || [];
        currentCart.push(cartItem);
        localStorage.setItem('cart', JSON.stringify(currentCart));
      }

      item.quantity = 1; // Reset quantity input after adding to cart
    },
    findCartItemById(id) {
      const currentCart = JSON.parse(localStorage.getItem('cart')) || [];
      return currentCart.find(item => item.id === id);
    }
  },
  computed: {
    items() {
      let filteredItems = [...this.filteredItems];
      if (this.nameFilter.trim() !== '') {
        filteredItems = filteredItems.filter(item =>
          item.name.toLowerCase().includes(this.nameFilter.toLowerCase())
        );
      }
      return filteredItems;
    }
  }
};
</script>

<style>
.active {
  border: 6px solid black !important;
}

.button-container {
  margin-top: 10px;
  margin-bottom: 10px;
}

.size-label {
  margin-right: 10px; /* Adjust as needed */
}

</style>
