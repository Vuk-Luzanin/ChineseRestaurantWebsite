<template>
  <div v-if="visible" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <button class="close-btn" @click="closeModal"><i class="fa-solid fa-x"></i></button>
      <img :src="dishImage" alt="Dish Image" class="modal-img">
      <h3>{{ dishName }}</h3>
      <h4 v-if="currentLanguage == 'English'"> Ingredients: {{ dishIngredients }}</h4> 
      <h4 v-if="currentLanguage == 'Srpski'"> Sastojci: {{ dishIngredients }}</h4>
      <div class="rating">
        <span v-for="n in 5" :key="n" @click="rate(n)" :class="{'rated': n <= rating}">★</span>
      </div>
      <div v-if="currentLanguage == 'English'">
        Average rating: {{ this.menuItems[this.dishId].mark }} ★
      </div>
      <div v-if="currentLanguage == 'Srpski'">
        Prosečna ocena: {{ this.menuItems[this.dishId].mark }} ★
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'DishView',
    props: {
        visible: {
            type: Boolean,
            required: true
        },
        dishImage: {
            type: String,
            required: true
        },
        dishName: {
            type: String,
            required: true
        },
        dishIngredients: { // Corrected name to match the prop
            type: String,
            required: true
        },
        dishId: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            rating: 0, // mark
            menuItems: [],
            currentLanguage: 'English',
        }
    },
    created() {
      this.menuItems = JSON.parse(localStorage.getItem('menu'));
      // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
    },
    methods: {
        closeModal() {
            this.$emit('close');
        },
        rate(n) {
            this.rating = n;
            this.menuItems[this.dishId].numOfMarks++;
            this.menuItems[this.dishId].mark = (this.menuItems[this.dishId].mark * (this.menuItems[this.dishId].numOfMarks - 1) + n) / this.menuItems[this.dishId].numOfMarks;
            localStorage.setItem('menu', JSON.stringify(this.menuItems));
        }
    }
}
</script>

<style>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  position: relative;
  font-size: 2rem;
}
.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
}
.modal-img {
  max-width: 55%;
  height: auto;
}
.rating {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
.rating span {
  font-size: 2rem;
  cursor: pointer;
}
.rated {
  color: gold;
}
</style>
