<template>
  <div>
    <NavigationView></NavigationView>
    <router-view/>
    <FooterView></FooterView>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
import NavigationView from './components/NavigationView.vue'
import FooterView from './components/FooterView.vue'

export default {

  components: {
    NavigationView, FooterView
  },
  created(){
    if (localStorage.getItem('menu') == null) {
      let menu = [
    { id: 0, name: "Chicken Wings", namesrb: "Krilca od pileta", category: "appetizer", categorysrb: "predjelo", img: "images/appetizer/chicken_wings.jpg", price: "10", mark: 0, numOfMarks: 0, ingredients: 'Krilca od pileta, soja sos, beli luk, đumbir, med', ingredientssrb: 'Krilca od pileta, soja sos, beli luk, đumbir, med' },
    { id: 1, name: "Crab Rangoon", namesrb: "Rangoon sa rakom", category: "appetizer", categorysrb: "predjelo", img: "images/appetizer/crab_rangoon.jpg", price: "12", mark: 0, numOfMarks: 0, ingredients: 'Rak mesa, krem sir, zeleni luk, Worcestershire sos, kore za wonton', ingredientssrb: 'Rak mesa, krem sir, zeleni luk, Worcestershire sos, kore za wonton' },
    { id: 2, name: "Tofu Soup", namesrb: "Supa sa tofuom", category: "appetizer", categorysrb: "predjelo", img: "images/appetizer/tofu_soup.jpg", price: "12", mark: 0, numOfMarks: 0, ingredients: 'Tofu, pečurke, spanać, soja sos, povrćna supa', ingredientssrb: 'Tofu, pečurke, spanać, soja sos, povrćna supa' },

    { id: 3, name: "Hot Pot", namesrb: "Vruća šerpa", category: "main-dish", categorysrb: "glavno jelo", img: "images/main-dishes/hot_pot.jpeg", price: "19", mark: 0, numOfMarks: 0, ingredients: 'Rezanci od goveđeg mesa, tofu, pekinški kupus, pečurke, bujon za vruću šerpu', ingredientssrb: 'Rezanci od goveđeg mesa, tofu, pekinški kupus, pečurke, bujon za vruću šerpu' },
    { id: 4, name: "Kung Pao Chicken", namesrb: "Kung Pao piletina", category: "main-dish", categorysrb: "glavno jelo", img: "images/main-dishes/kung_pao_chicken.jpg", price: "23", mark: 0, numOfMarks: 0, ingredients: 'Pileće grudi, kikiriki, paprike, sušene crvene papričice, soja sos', ingredientssrb: 'Pileće grudi, kikiriki, paprike, sušene crvene papričice, soja sos' },
    { id: 5, name: "Peking Roast Duck", namesrb: "Pekinški pečeni patka", category: "main-dish", categorysrb: "glavno jelo", img: "images/main-dishes/peking_roast_duck.jpg", price: "26", mark: 0, numOfMarks: 0, ingredients: 'Patka, hoisin sos, mladi luk, krastavci, kineske palačinke', ingredientssrb: 'Patka, hoisin sos, mladi luk, krastavci, kineske palačinke' },

    { id: 6, name: "Mango Psudding", namesrb: "Mango puding", category: "dessert", categorysrb: "dezert", img: "images/desserts/mango_pudding.jpg", price: "6", mark: 0, numOfMarks: 0, ingredients: 'Pire od manga, želatin, šećer, mleko, šlag', ingredientssrb: 'Pire od manga, želatin, šećer, mleko, šlag' },
    { id: 7, name: "Moon Cake", namesrb: "Mesečev kolač", category: "dessert", categorysrb: "dezert", img: "images/desserts/moon_cake.jpg", price: "8", mark: 0, numOfMarks: 0, ingredients: 'Pasta od lotosovog semena, slani žumanca, brašno, zlatni sirup, alkalna voda', ingredientssrb: 'Pasta od lotosovog semena, slani žumanca, brašno, zlatni sirup, alkalna voda' },
    { id: 8, name: "Tang Yuan", namesrb: "Tang Yuan", category: "dessert", categorysrb: "dezert", img: "images/desserts/tang_yuan.jpg", price: "7", mark: 0, numOfMarks: 0, ingredients: 'Brašno od glutinoznog pirinča, pasta od crnog susama, šećer, voda, sirup od đumbira', ingredientssrb: 'Brašno od glutinoznog pirinča, pasta od crnog susama, šećer, voda, sirup od đumbira' }
];



      localStorage.setItem('menu', JSON.stringify(menu))
    } 
  }
}
</script>
