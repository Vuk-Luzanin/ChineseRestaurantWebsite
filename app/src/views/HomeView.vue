<template>
  <div class="home">
    <section class="home">
      <Swiper 
        :effect="'flip'"
        :grabCursor="true"
        :modules="modules"
        :options="swiperOptions" 
        class="home-slider">
        <SwiperSlide v-for="(slide, index) in slides" :key="index" class="swiper-slide slide">
          <div class="content">
            <span class="cat">
              <router-link to="/menu" v-if="currentLanguage == 'English'">
                order online
              </router-link>
              <router-link to="/menu" v-if="currentLanguage == 'Srpski'">
                naruči online
              </router-link>
            </span>
            <h3 v-if="currentLanguage == 'English'">{{ slide.title }}</h3>
            <h3 v-if="currentLanguage == 'Srpski'">{{ slide.titlesrb }}</h3>
            <router-link to="/menu" class="btn" v-if="currentLanguage == 'English'">see menu</router-link>
            <router-link to="/menu" class="btn" v-if="currentLanguage == 'Srpski'">vidi meni</router-link>
          </div>
          <div class="image">
            <img :src="require(`../assets/images/${slide.image}`)" :alt="slide.alt">
          </div>
        </SwiperSlide>
      </Swiper>
    </section>

    <section class="category">
      <div class="box-container">
        <span class="box" :style="category == 'appetizer' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-1.png" alt="Page1">
          <h3 v-if="currentLanguage == 'English'">appetizer</h3>
          <h3 v-if="currentLanguage == 'Srpski'">predjela</h3>
        </span>
      
        <span class="box" :style="category == 'main-dish' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-2.png" alt="Page2">
          <h3 v-if="currentLanguage == 'English'">main-dish</h3>
          <h3 v-if="currentLanguage == 'Srpski'">glavna jela</h3>
        </span>
      
        <span class="box" :style="category == 'dessert' ? {border: activeBorder } : {}">
          <img src="../assets/images/menu/cat-3.png" alt="Page3">
          <h3 v-if="currentLanguage == 'English'">desserts</h3>
          <h3 v-if="currentLanguage == 'Srpski'">dezerti</h3>
        </span>
      </div>
    </section>

    <section class="products">
      <h1 class="title" v-if="currentLanguage == 'English'">best rated dishes</h1>
      <h1 class="title" v-if="currentLanguage == 'Srpski'">najbolje ocenjena jela</h1>
      <div class="box-container">
        <form class="box" v-for="item in bestRatedItems" :key="item.id">
          <button class="fas fa-eye" type="button" @click="showQuickView(item)"></button>
          <img :src="require(`@/assets/${item.img}`)">
          <p class="cat" @click="filter(item.category)" v-if="currentLanguage == 'English'">{{item.category}}</p>
          <p class="cat" @click="filter(item.category)" v-if="currentLanguage == 'Srpski'">{{item.categorysrb}}</p>
          <div class="name" v-if="currentLanguage == 'English'">{{item.name}}</div>
          <div class="name" v-if="currentLanguage == 'Srpski'">{{item.namesrb}}</div>
          <div class="flex">
            <div class="price"><span>$</span>{{item.price}}<span>/-</span></div>
          </div>
        </form>
      </div>
    </section>

    <div class="btn">
      <router-link to="/menu" v-if="currentLanguage == 'Srpski'">vidi sve</router-link>
      <router-link to="/menu" v-if="currentLanguage == 'English'">view all</router-link>
    </div>

    <DishView 
      v-if="showModal"
      :visible="showModal" 
      :dishImage="modalImage" 
      :dishName="modalName"
      :dishIngredients="modalIngredients"
      :dishId="modalId"
      @close="showModal = false"
    />
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/swiper-bundle.css';
import 'swiper/css';
import 'swiper/css/effect-flip';
import 'swiper/css/pagination';
import 'swiper/css/navigation';

import { EffectFlip, Pagination, Navigation } from 'swiper/modules';
import DishView from '../components/DishView.vue';

export default (await import('vue')).defineComponent({
  name: 'HomeView',
  components: {
    Swiper,
    SwiperSlide,
    DishView,
  },
  setup() {
    return {
      modules: [EffectFlip, Pagination, Navigation],
    }
  },
  data() {
    return {
      activeBorder: "6px solid black",
      category: "",
      menuItems: [],
      bestRatedItems: [],
      swiperOptions: {
        slidesPerView: 1,
        spaceBetween: 30,
        pagination: {
          clickable: true,
        },
        navigation: true,
        effect: 'flip',
      },
      slides: [
        { title: 'Crockpot Crispy Caramelized Pork Ramen Noodle Soup',titlesrb: 'Crockpot hrskava karamelizovana svinjetina u supi od ramen nudli', image: 'home/crockpot-crispy-caramelized-pork-ramen-noodle-soup.png', alt: 'Crockpot Crispy Caramelized Pork Ramen Noodle Soup' },
        { title: 'Soy & Butter-Glazed Chicken with Sesame Vegetables & White Rice',titlesrb: 'Piletina glazirana soja sosom i puterom sa susamom povrćem i belim pirinčem', image: 'home/soy-&-butter-glazed-chicken-with-sesame-vegetables-&-white-rice.png', alt: 'Soy & Butter-Glazed Chicken with Sesame Vegetables & White Rice' },
        { title: 'Thai Red Curry with Shrimp, Vegetables, and Infused Rice',titlesrb: 'Tai crveni kari sa škampima, povrćem i aromatizovanim pirinčem', image: 'home/thai-shrimp-red-curry-recipe-with-vegetables.png', alt: 'Thai Red Curry with Shrimp, Vegetables, and Infused Rice' },
      ],
      showModal: false,
      modalImage: '',
      modalName: '',
      modalIngredients: '',
      modalId: '',
      currentLanguage: 'English'
    }
  },
  created(){
    this.menuItems = JSON.parse(localStorage.getItem('menu'))
    // Sort menu items by rating and get top 3
    this.bestRatedItems = this.menuItems.sort((a, b) => b.mark - a.mark).slice(0, 3);

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
      this.category = category;
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
    }
  },
})
</script>

<style scoped>
.home-slider {
  width: 100%;
  height: 100%;
  cursor: grab;
}

.home-slider:active {
  cursor: grabbing;
}

.swiper-slide {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.content {
  font-size: 1.7rem !important;
  color:var(--light-color) !important;  
}

.image img {
  width: 100%;
  height: auto;
}

</style>
