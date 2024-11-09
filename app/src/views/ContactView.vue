<template>
    <div>
        <div class="heading" v-if="currentLanguage == 'English'">
        <h3>contact us</h3>
        <p><router-link to="/">home </router-link> <span> / contact</span></p>
        </div>
        <div class="heading" v-if="currentLanguage == 'Srpski'">
        <h3>Kontaktirajte nas</h3>
        <p><router-link to="/">početna </router-link> <span> / kontakt</span></p>
        </div>

        <section class="contact">

            <div class="row">

                <div class="image">
                    <img src="../assets/images/contact/contact-img.svg" alt="">
                </div>

                <form action="" method="post" v-if="currentLanguage == 'English'">
                    <h3>tell us something!</h3>
                    <input type="text" name="name" required placeholder="enter your name" maxlength="50" class="box">
                    <input type="number" name="number" required placeholder="enter your number" max="9999999999" min="0" class="box" onkeypress="if(this.value.length == 10) return false;">
                    <input type="email" name="email" required placeholder="enter your email" maxlength="50" class="box">
                    <textarea name="msg" placeholder="enter your message" required class="box" cols="30" rows="10" maxlength="500"></textarea>
                    <input type="submit" value="send message" class="btn" name="send">
                </form>
                <form action="" method="post" v-if="currentLanguage == 'Srpski'">
                    <h3>recite nam nešto!</h3>
                    <input type="text" name="name" required placeholder="unesite Vaše ime" maxlength="50" class="box">
                    <input type="number" name="number" required placeholder="unesti broj telefona" max="9999999999" min="0" class="box" onkeypress="if(this.value.length == 10) return false;">
                    <input type="email" name="email" required placeholder="unesite email adresu" maxlength="50" class="box">
                    <textarea name="msg" placeholder="unesite poruku" required class="box" cols="30" rows="10" maxlength="500"></textarea>
                    <input type="submit" value="pošaljite poruku" class="btn" name="send">
                </form>

            </div>

        </section>
    </div>
</template>

<script>

export default {
    name: 'ContactView',
    data() {
        return {
            currentLanguage: 'English'
        }
    },
    created() {
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
