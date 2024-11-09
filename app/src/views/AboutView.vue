<template>
    <div>
        <div class="heading">
            <h3 v-if="currentLanguage == 'English'">about us</h3>
             <h3 v-if="currentLanguage == 'Srpski'"> info</h3>
            <p v-if="currentLanguage == 'English'"><router-link to="/">home</router-link> <span> / about</span></p>
            <p v-if="currentLanguage == 'Srpski'"><router-link to="/">početna</router-link> <span> / info</span></p>
        </div>

        <section class="about">
            <div class="row">

                <div class="image">
                    <img src="../assets/images/about/about-img.svg" alt="Page">
                </div>

                <div class="content">
                    <h3 v-if="currentLanguage == 'English'">why choose us?</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">zašto da izaberete nas?</h3>
                    <p v-if="currentLanguage == 'English'">At our restaurant, we bring authentic Chinese flavors right to your table. Our chefs use the freshest ingredients and traditional recipes to create a culinary experience that transports you to the heart of China. With a warm, welcoming atmosphere and exceptional service, we strive to make every meal unforgettable. Choose us for our dedication to quality, passion for great food, and a truly unique dining adventure.</p>
                    <p v-if="currentLanguage == 'Srpski'">Naš restoran vam donosi autentične kineske ukuse direktno na vaš sto. Naši kuvari koriste najsvježije sastojke i tradicionalne recepte kako bi stvorili kulinarsko iskustvo koje vas prenosi u srce Kine. Sa toplom, gostoljubivom atmosferom i izuzetnom uslugom, trudimo se da svaki obrok bude nezaboravan. Izaberite nas zbog naše posvećenosti kvalitetu, strasti prema odličnoj hrani i zaista jedinstvenog kulinarskog doživljaja.</p>

                    <router-link to="/menu" class="btn" v-if="currentLanguage == 'English'">our menu</router-link>
                    <router-link to="/menu" class="btn" v-if="currentLanguage == 'Srpski'">naš meni</router-link>
                </div>
                

            </div>

        </section>

         <section class="about">
            <div class="row">

                <div class="content">
                    <h3 v-if="currentLanguage == 'English'">Our awards?</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">Naše nagrade?</h3>
                    <p v-if="currentLanguage == 'English'">We are honored to share that our Chinese restaurant has been awarded a Michelin star, recognizing our commitment to exceptional culinary standards. This prestigious accolade highlights our dedication to crafting authentic Chinese cuisine with the finest ingredients and meticulous preparation. We invite you to join us and experience the extraordinary flavors and impeccable service that earned us this esteemed recognition.</p>
                    <p v-if="currentLanguage == 'Srpski'">Sa ponosom delimo vest da je naš kineski restoran nagrađen Mišlenovom zvezdom, što priznaje našu posvećenost izuzetnim kulinarskim standardima. Ovo prestižno priznanje ističe našu predanost kreiranju autentične kineske kuhinje sa najfinijim sastojcima i pažljivom pripremom. Pozivamo vas da nam se pridružite i doživite izvanredne ukuse i besprekornu uslugu koja nam je donela ovaj ugledni status.</p>
                    <a href="https://guide.michelin.com/rs/en/restaurants" class="btn" v-if="currentLanguage == 'English'">Michelin Star Restaurants</a>
                    <a href="https://guide.michelin.com/rs/en/restaurants" class="btn" v-if="currentLanguage == 'Srpski'">Restorani sa Michelinovom zvezdicom</a>
                </div>

                <div class="image">
                    <img src="../assets/images/about/star.jpg" alt="Page">
                </div>
                

            </div>

        </section>

        <h1 class="title" v-if="currentLanguage == 'English'">3 simple steps</h1>
        <h1 class="title" v-if="currentLanguage == 'Srpski'">3 jednostavna koraka</h1>

        <section class="steps">

            <div class="box-container">

                <span class="box">
                    <img src="../assets/images/steps/step-1.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">select food</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">Izaberi</h3>
                    <p v-if="currentLanguage == 'English'">Enjoy a wide range of delicious Chinese dishes. From tasty soups to flavorful noodles and fresh seafood, each dish is made with care and quality ingredients. Discover the wonderful flavors that make our food special.</p>
                    <p v-if="currentLanguage == 'Srpski'">Uživajte u širokom spektru ukusnih kineskih jela. Od ukusnih supa, preko aromatičnih nudli do svežih morskih plodova, svako jelo je pripremljeno s pažnjom i kvalitetnim sastojcima. Otkrijte divne ukuse koji čine našu hranu posebnom.</p>

                </span>

                <span class="box">
                    <img src="../assets/images/steps/step-2.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">30 minutes delivery</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">dostava je za 30 minuta</h3>
                    <p v-if="currentLanguage == 'English'">Get your favorite Chinese food delivered to your door in just 30 minutes. Our fast and reliable service ensures your meal arrives hot and fresh. Enjoy a quick and convenient dining experience without leaving your home.</p>
                    <p v-if="currentLanguage == 'Srpski'">Naručite svoju omiljenu kinesku hranu i uživajte u dostavi na vaša vrata za samo 30 minuta. Naša brza i pouzdana usluga garantuje da će vaš obrok stići topao i svež. Uživajte u brzom i praktičnom gastronomskom iskustvu bez napuštanja doma.</p>

                </span>

                <span class="box">
                    <img src="../assets/images/steps/step-3.png" alt="">
                    <h3 v-if="currentLanguage == 'English'">enjoy food!</h3>
                    <h3 v-if="currentLanguage == 'Srpski'">uživajte u hrani!</h3>
                    <p v-if="currentLanguage == 'English'">Savor the delicious taste of our Chinese cuisine. Each dish is made with fresh ingredients and traditional recipes. Relax and enjoy a wonderful dining experience with every bite, whether you're dining in or taking out.</p>
                    <p v-if="currentLanguage == 'Srpski'">Uživajte u ukusu naše ukusne kineske kuhinje. Svaki obrok je pripremljen od svežih sastojaka i po tradicionalnim receptima. Opustite se i uživajte u predivnom gastronomskom iskustvu sa svakim zalogajem, bez obzira da li jedete u restoranu ili nosite hranu sa sobom.</p>

                </span>

            </div>

        </section>

        <section class="reviews">

            <h1 class="title" v-if="currentLanguage == 'English'">customer's reviews</h1>
            <h1 class="title" v-if="currentLanguage == 'Srpski'">ocene gostiju</h1>

             <swiper class="reviews-slider" :breakpoints="breakpoints" :space-between="50" @swiper="onSwiper" @slideChange="onSlideChange" :pagination="pagination">
                <swiper-slide class="slide">
                    <img src="../assets/images/appetizer/chicken_wings.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">The flavors here are just incredible! Each dish feels like a trip to China. The ingredients are fresh, and the presentation is always beautiful. It's my go-to spot for authentic Chinese cuisine.</p>
                    <p v-if="currentLanguage == 'Srpski'">Ukus ovde je neverovatan! Svako jelo je kao putovanje u Kinu. Sastojci su sveži, a prezentacija uvek predivna. Ovo je moje omiljeno mesto za autentičnu kinesku kuhinju.</p>
                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star-half-alt"></i>
                    </div>
                    <h3>Wěi qí (伟祺)</h3>
                </swiper-slide>
                <swiper-slide class="slide">
                    <img src="../assets/images/appetizer/tofu_soup.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">I've never had a bad meal here. The service is quick, and the staff is always friendly. I especially love the dumplings and the sweet and sour chicken. Highly recommend this place!</p>
                    <p v-if="currentLanguage == 'Srpski'">Nikad nisam imao loš obrok ovde. Usluga je brza, a osoblje uvek ljubazno. Posebno volim njihove knedle i slatko-kiselo pile. Toplo preporučujem ovo mesto!</p>

                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                    </div>
                    <h3>Bruce Lee (李小龍)</h3>
                </swiper-slide>
                <swiper-slide class="slide">
                    <img src="../assets/images/desserts/tang_yuan.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">Amazing food and atmosphere! The restaurant is cozy and perfect for a date night. The Peking duck is a must-try, crispy and delicious. We loved every bite and can't wait to come back.</p>
                    <p v-if="currentLanguage == 'Srpski'">Fantastična hrana i atmosfera! Restoran je ušuškan i savršen za veče u dvoje. Pekinška patka je nešto što morate probati, hrskava i ukusna. Uživali smo u svakom zalogaju i jedva čekamo da se vratimo.</p>
                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                    </div>
                    <h3>Huang (黄)</h3>
                </swiper-slide>
                <swiper-slide class="slide">
                    <img src="../assets/images/desserts/moon_cake.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">This place is a gem! The lunch specials are a great deal, and you get a lot of food for the price. Everything tastes fresh, and the flavors are spot on. I'll be back for sure.</p>
                    <p v-if="currentLanguage == 'Srpski'">Ovo mesto je prava riznica! Ručak specijali su odlična ponuda, dobijete puno hrane za cenu. Sve je sveže i ukusi su baš onakvi kakvi treba da budu. Sigurno se vraćam.</p>

                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star-alt"></i>
                    </div>
                    <h3>Zhao (赵)</h3>
                </swiper-slide>
                <swiper-slide class="slide">
                    <img src="../assets/images/appetizer/chicken_wings.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">I love the variety on the menu. Whether I'm in the mood for something spicy or something mild, they always have the perfect dish. The seafood options are particularly good.</p>
                    <p v-if="currentLanguage == 'Srpski'">Volim raznovrsnost na meniju. Bez obzira da li sam raspoložen za nešto ljuto ili nešto blago, uvek imaju savršeno jelo. Posebno su dobre opcije sa morskim plodovima.</p>

                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star-half-alt"></i>
                    </div>
                    <h3>Chen (陈)</h3>
                </swiper-slide>
                <swiper-slide class="slide">
                    <img src="../assets/images/appetizer/chicken_wings.jpg" alt="">
                    <p v-if="currentLanguage == 'English'">The best Chinese restaurant in town! The food is always hot and tasty, and the delivery is super fast. The staff is courteous, and the overall experience is fantastic every time.</p>
                    <p >Najbolji kineski restoran u gradu! Hrana je uvek vruća i ukusna, a dostava je veoma brza. Osoblje je ljubazno, a ukupno iskustvo je fantastično svaki put.</p>

                    <div class="stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star-half-alt"></i>
                    </div>
                    <h3>Wang (王)</h3>
                </swiper-slide>
            </swiper>
        </section>
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3320.052477449523!2d20.473560436546734!3d44.80541271980541!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x475a7a9f5ee145d3%3A0x3ed89b5bb505d83!2sUniversity%20of%20Belgrade%20School%20of%20Electrical%20Engineering!5e0!3m2!1sen!2srs!4v1731160580084!5m2!1sen!2srs" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>      
    </div>
</template>



<style scoped>
@import 'swiper/swiper-bundle.css';

.swiper-container {
  width: 100%;
  height: 100%;
}
</style>
<script>

    import { Swiper, SwiperSlide, Pagination } from 'swiper/vue';
    // Import Swiper styles
    import 'swiper/css';

export default {
    name: 'AboutView',
    components: {
      Swiper,
      SwiperSlide,
    },
    data () {
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
    },
    setup() {
      const onSwiper = (swiper) => {
        console.log(swiper);
      };
      const onSlideChange = () => {
        console.log('slide change');
      };
      
      return {
        onSwiper,
        onSlideChange,
        modules: [Swiper, SwiperSlide, Pagination],
        pagination: {
            el: '.swiper-pagination',
            clickable: true,
        },
        breakpoints: {
            550: {
                slidesPerView: 2,
            },
            768: {
                slidesPerViewslides: 2,
            },
            1024: {
                slidesPerView: 3,
            },
        },
      };
    },
  };
</script>


<style scoped>
    @import 'swiper/swiper-bundle.css';

    .swiper-container {
        width: 100%;
        height: 100%;
    }

    .swiper-pagination {
        position: absolute;
        text-align: center;
        transition: 300ms opacity;
        transform: translate3d(0, 0, 0);
        z-index: 10;
        bottom: 10px; 
        width: 100%;
    }
</style>