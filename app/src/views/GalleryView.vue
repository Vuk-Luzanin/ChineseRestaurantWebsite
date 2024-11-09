<template>
<div>
  <div class="heading">
          <h3 v-if="currentLanguage == 'English'">Gallery</h3>
          <h3 v-if="currentLanguage == 'Srpski'">Galerija</h3>
          <p v-if="currentLanguage == 'English'"><router-link to="/">home</router-link> <span> / gallery</span></p>
          <p v-if="currentLanguage == 'Srpski'"><router-link to="/">početna</router-link> <span> / galerija</span></p>
      </div>
    <div class="gallery-container">
        <div class="gallery">
          <div v-for="image in images" :key="image.id" class="image-container">
            <img :src="require(`../assets/images/${image.src}`)" :alt="image.alt" />
          </div>
        </div>
  </div>
</div>

  
</template>

<script>
export default {
  name: 'GalleryView',
  data() {
    return {
      images: [
        { id: 1, src: 'gallery/slika1.jpeg', alt: 'Image 1' },
        { id: 2, src: 'gallery/slika2.jpeg', alt: 'Image 2' },
        { id: 3, src: 'gallery/slika3.jpeg', alt: 'Image 3' },
        { id: 4, src: 'gallery/slika4.jpeg', alt: 'Image 4' },
        { id: 5, src: 'gallery/slika5.jpeg', alt: 'Image 5' },
        { id: 6, src: 'gallery/slika6.jpeg', alt: 'Image 6' }
      ],
      currentLanguage: 'English',
    };
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
};
</script>

<style scoped>
.gallery-container {
  display: flex;
  justify-content: center;
  padding: 20px;
}

.gallery {
  width: 90%; /* Adjust the percentage to make the grid occupy more space */
  max-width: 1200px; /* Optional: to limit the maximum width of the grid */
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 10px;
}

.image-container {
  width: 100%;
  height: 200px; /* Adjust the height as needed */
  overflow: hidden;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.image-container:hover img {
  transform: scale(1.1);
}
</style>
