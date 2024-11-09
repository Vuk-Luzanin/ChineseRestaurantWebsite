<template>
   <div>
      <header class="header">
         <section class="flex">
            <img src="@/assets/images/logo/logo.png" alt="Logo" style="width: 5%">
            <router-link to="/" class="logo">Dragon Warrior<br /> Noodles & Tofu</router-link>

            <!-- Dugme za jezik -->
            <button @click="toggleLanguageMenu" class="selected-language">
               {{ currentLanguage }} <i class="fas fa-chevron-down"></i>
            </button>

            <!-- Modalni prozor za jezik -->
            <div v-if="isLanguageModalVisible" class="profile-modal" >
               <button @click="toggleLanguageMenu" class="close-btn">&times;</button>
               <div>
                  <button class="btn" @click="switchLanguage('en')">English</button>
                  <button class="btn" @click="switchLanguage('sr')">Srpski</button>
               </div>
            </div>

            <!-- Navbar -->
            <nav class="navbar" :class="{ active: isMenuActive }">
               <router-link to="/" v-if="currentLanguage == 'English'">home</router-link>
               <router-link to="/" v-if="currentLanguage == 'Srpski'">početna</router-link>
               <router-link to="/about" v-if="currentLanguage == 'English'">about</router-link>
               <router-link to="/about" v-if="currentLanguage == 'Srpski'">info</router-link>
               <router-link to="/gallery" v-if="currentLanguage == 'English'">gallery</router-link>
               <router-link to="/gallery" v-if="currentLanguage == 'Srpski'">galerija</router-link>
               <router-link to="/menu" v-if="currentLanguage == 'English'">menu</router-link>
               <router-link to="/menu" v-if="currentLanguage == 'Srpski'">meni</router-link>
               <router-link to="/orders" v-if="currentLanguage == 'English'">orders</router-link>
               <router-link to="/orders" v-if="currentLanguage == 'Srpski'">narudžbine</router-link>
               <router-link to="/contact" v-if="currentLanguage == 'English'">contact</router-link>
               <router-link to="/contact" v-if="currentLanguage == 'Srpski'">kontakt</router-link>
            </nav>

            <!-- Ikone -->
            <div class="icons">
               <router-link to="/cart"><i class="fas fa-shopping-cart"></i><span></span></router-link>
               <div id="user-btn" class="fas fa-user" @click="toggleProfileModal"></div>
               <div @click="toggleMenu" id="menu-btn" class="fas fa-bars"></div>
            </div>

            <!-- Modalni prozor za profil -->
            <div v-if="isProfileModalVisible" class="profile-modal">
               <button @click="toggleProfileModal" class="close-btn">&times;</button>
               <p class="name">{{ username }}</p>
               <div class="flex">
                  <router-link to="/profile" class="btn" v-if="currentLanguage == 'English'">Profile</router-link>
                  <router-link to="/profile" class="btn" v-if="currentLanguage == 'Srpski'">Profil</router-link>
                  <button @click="logout()" class="btn delete-btn" v-if="currentLanguage == 'English'">Logout</button>
                  <button @click="logout()" class="btn delete-btn" v-if="currentLanguage == 'Srpski'">Izloguj se</button>
               </div>
               <p class="account">
                  <router-link to="/login" v-if="currentLanguage == 'English'">Login</router-link> 
                  <router-link to="/login" v-if="currentLanguage == 'Srpski'">Uloguj se</router-link> 
                  <span v-if="currentLanguage == 'English'">&nbsp; or &nbsp;</span> 
                  <span v-if="currentLanguage == 'Srpski'">&nbsp; or &nbsp;</span> 
                  <router-link to="/register" v-if="currentLanguage == 'English'">Register</router-link>
                  <router-link to="/register" v-if="currentLanguage == 'Srpski'">Registruj se</router-link>
               </p>
            </div>
         </section>  
      </header>
   </div>
</template>

<script>
export default {
   name: 'NavigationView',
   data() {
      return {
         isMenuActive: false,
         isProfileModalVisible: false,
         user: null,
         username: '',
         isLanguageModalVisible: false,
         currentLanguage: 'English'
      }
   },
   methods: {
      toggleMenu() {
         this.isMenuActive = !this.isMenuActive;
      },
      toggleProfileModal() {
         this.isProfileModalVisible = !this.isProfileModalVisible;
         const userData = localStorage.getItem('user');
         if (userData) {
            try {
               this.user = JSON.parse(userData);
               this.username = this.user.name;
            } catch (error) {
               console.error('Error parsing user data:', error);
               this.username = 'Not logged in';
            }
         } else {
            this.username = 'Not logged in';
         }
      },
      logout() {
         localStorage.removeItem('user');
         this.username = 'Not logged in';
         this.isProfileModalVisible = false;
      },
      toggleLanguageMenu() {
         this.isLanguageModalVisible = !this.isLanguageModalVisible;
      },
      switchLanguage(language) {
         if (language === 'sr') {
            this.currentLanguage = 'Srpski';
         } else {
            this.currentLanguage = 'English';
         }
         localStorage.setItem('language', language);
         this.isLanguageModalVisible = false; // Zatvara modalni prozor za jezik nakon izbora jezika
         // Opcionalno: Ponovno učitavanje stranice
          window.location.reload();
      }
   },
   created() {
      const userData = localStorage.getItem('user');
      if (userData) {
         try {
            this.user = JSON.parse(userData);
            this.username = this.user.name;
         } catch (error) {
            console.error('Error parsing user data:', error);
            this.username = 'Not logged in';
         }
      } else {
         this.username = 'Not logged in';
      }

      // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
   }
}
</script>

<style scoped>
/* Stilovi za modalni prozor profila i jezika */
.profile-modal {
   position: absolute;
   top: 60px; /* Prilagodite na osnovu visine zaglavlja */
   right: 10px;
   background: white;
   border: 2px solid black;
   padding: 20px;
   box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
   z-index: 1000;
   font-size: 1.5rem;
}

.profile-modal .close-btn {
   position: absolute;
   top: 10px;
   right: 10px;
   background: none;
   border: none;
   font-size: 1.5rem;
   cursor: pointer;
}

.profile-modal .name {
   font-size: 1.2em;
   margin-bottom: 10px;
}

.profile-modal .flex {
   display: flex;
   gap: 10px;
   margin-bottom: 10px;
}

.profile-modal .btn {
   padding: 10px 20px;
   border: none;
   cursor: pointer;
}

.profile-modal .btn.delete-btn {
   background: #e74c3c;
   color: white;
}

.profile-modal .account {
   text-align: center;
}

.profile-modal .account a {
   color: #3498db;
   text-decoration: none;
}

.selected-language {
   display: flex;
   align-items: center;
   cursor: pointer;
   background-color: var(--yellow); /* Prilagođena boja pozadine */
   color: #fff;
   border: none;
   border-radius: 4px;
   padding: 8px 16px;
   transition: background-color 0.3s ease;
}

.selected-language:hover {
   background-color: #2980b9; /* Prilagođena boja pri hoveru */
}

.selected-language i {
   margin-left: 5px;
   font-size: 0.75em;
}

.language-modal {
   position: absolute;
   top: 100%; /* Prilagodite poziciju u odnosu na dugme za jezik */
   right: 0;
   background-color: #fff;
   border: 1px solid #ccc;
   border-radius: 4px;
   box-shadow: 0 2px 4px rgba(0,0,0,0.1);
   list-style-type: none;
   padding: 4px 0;
   margin: 0;
   display: none; /* Prikaz kontrolisan preko v-if */
   z-index: 1000; /* Povećajte z-index ako je potrebno */
}

.language-menu li {
   padding: 4px 8px;
}

.language-menu li button {
   background: none;
   border: none;
   cursor: pointer;
   font-size: inherit;
   color: #333;
   transition: background-color 0.3s ease;
}

.language-menu li button:hover {
   background-color: #f0f0f0;
}

.language-modal button {
   display: block;
   width: 100%;
   text-align: center;
   padding: 8px 0;
   margin-bottom: 5px; /* Dodajte razmak između dugmadi */
}
</style>
