<template>
    <div>
         <div class="heading" v-if="currentLanguage == 'English'">
            <h3>your profile</h3>
            <p><router-link to="/">home</router-link> <span> / profile</span></p>
        </div>
        <div class="heading" v-if="currentLanguage == 'Srpski'">
            <h3>vaš profil</h3>
            <p><router-link to="/">početna</router-link> <span> / profil</span></p>
        </div>
        <section class="user-details">

        <div class="user">
            <img src="../assets/images/profile/user-icon.png" alt="">
            <p><i class="fas fa-user"></i> <span>{{username}}</span></p>
            <p><i class="fas fa-phone"></i> <span>{{phone}}</span></p>
            <p><i class="fas fa-envelope"></i> <span>{{mail}}</span></p>
            <!-- <a href="update_profile.html" class="btn">update profile</a> -->
            <p class="address"><i class="fas fa-map-marker-alt"></i> <span>{{address}}</span></p>
            <!-- <a href="update_address.html" class="btn">update address</a> -->
        </div>

        </section>
    </div>
</template>


<script>

export default {
   name: 'ProfileView',
   data() {
    return {
        username: '',
        phone: '',
        mail: '',
        address: '',
        currentLanguage:'English',
    }
   },
   created() {
      if (localStorage.getItem('user') == null) {
         this.username = 'Not logged in';
      } else {
         this.user = JSON.parse(localStorage.getItem('user'));
         this.username = this.user.name;
         this.phone = this.user.phone;
         this.mail = this.user.mail;
         this.address = this.user.address;
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
