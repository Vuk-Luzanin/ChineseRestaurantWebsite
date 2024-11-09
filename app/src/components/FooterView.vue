<template>
    <div>
        <footer class="footer">

            <section class="box-container">

                <span class="box">
                    <img src="../assets/images/footer/email-icon.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">our email</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">naš mejl</h3>
                    <a href="mailto:nd220076d@student.etf.bg.ac.rs">nd220076d@etf.bg.ac.rs</a>
                    <a href="mailto:lv220029d@student.etf.bg.ac.rs">lv220029d@etf.bg.ac.rs</a>
                </span>

                <span class="box">
                    <img src="../assets/images/footer/clock-icon.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">opening hours</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">Radno vreme</h3>
                    <p v-if="currentLanguage == 'English'">11:00am to 23:00pm </p>
                    <p v-if="currentLanguage == 'Srpski'">11:00am do 23:00pm </p>
                    <p v-if="currentLanguage == 'English'">14:00am to 00:00pm weekend</p>
                    <p v-if="currentLanguage == 'Srpski'">14:00am do 00:00pm vikendom</p>
                </span>

                <span class="box">
                    <img src="../assets/images/footer/map-icon.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">our address</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">naša adresa</h3>
                    <a href="https://www.google.com/maps">Novi Pazar, Serbia</a>
                    <a href="https://www.google.com/maps">Čačak, Serbia</a>
                </span>

                <span class="box">
                    <img src="../assets/images/footer/phone-icon.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">our number</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">Telefon</h3>
                    <a href="tel:381 62 1666 937">+381 62 1666 937</a>
                    <a href="tel:381 69 607 839">+381 69 607 839</a>
                </span>

            </section>

            <div v-if="currentLanguage == 'English'" class="credit">&copy; copyright @ 2024 by <span>Nušević Davud, Lužanin Vuk</span> | Department of Software Engineering, School of Electrical Engineering, University of Belgrade</div>
            <div v-if="currentLanguage == 'Srpski'" class="credit">&copy; copyright @ 2024 od <span>Nušević Davud, Lužanin Vuk</span> | Odsek za softversko inženjerstvo, Elektrotehnički fakultet, Univerzitet u Beogradu</div>

        </footer>
    </div>
</template>

<script>
export default {
    name: 'FooterView',
    data() {
        return {
            currentLanguage: 'English',
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
