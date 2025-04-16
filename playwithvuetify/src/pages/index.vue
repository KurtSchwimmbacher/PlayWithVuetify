<template>
  <v-app>
    <v-app-bar :elevation="24">
      <template #prepend>
        <v-app-bar-nav-icon />
      </template>
      <v-app-bar-title>Kurts Movie Posters</v-app-bar-title>
      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>

      <!-- Hero Section -->
      <v-parallax
        :src="grungeTexture"
        height="600"
        cover
        class="d-flex align-center justify-center"
      >
        <div class="text-white text-center">
          <h1 class="text-h3 font-weight-bold">Welcome to Kurt's Posters</h1>
          <p class="text-subtitle-1">A showcase of visual stories</p>
        </div>
      </v-parallax>


      <v-divider :thickness="3" class="my-4"></v-divider>

      <v-container>
        <v-row justify="center" class="mb-4">
          <v-chip
            v-for="category in categories"
            :key="category"
            @click="selectedCategory = category"
            :color="selectedCategory === category ? 'primary' : 'default'"
            class="ma-2"
            variant="elevated"
            clickable
          >
            {{ category }}
          </v-chip>
          <v-chip
            @click="selectedCategory = null"
            :color="!selectedCategory ? 'primary' : 'default'"
            class="ma-2"
            variant="elevated"
            clickable
          >
            All
          </v-chip>
        </v-row>
      </v-container>


      <!-- Poster Grid -->
      <v-container>
        <v-row>
          <v-col v-for="(poster, index) in filteredPosters" :key="index" cols="12" sm="6" md="4">
            <v-card elevation="4">
              <v-img :src="poster.src" height="400" cover></v-img>
              <v-card-title class="text-h6">
                {{ poster.title }}
              </v-card-title>
            </v-card>
          </v-col>
        </v-row>
      </v-container>



      <v-divider class="my-8" />
      <v-container class="py-8 px-6 rounded-xl elevation-1 bg-grey-darken-3">
        <v-row align="center">
          <!-- Left Column -->
          <v-col cols="12" md="6">
            <h2 class="text-h5 font-weight-bold">Stay in the loop!</h2>
            <p class="text-body-1">
              Subscribe to Kurt's Movie Poster newsletter for new additions, behind-the-scenes details, and exclusive content.
            </p>
          </v-col>

          <!-- Right Column (Form) -->
          <v-col cols="12" md="6">
            <v-form @submit.prevent="submitNewsletter">
              <v-text-field
                v-model="email"
                label="Your Email"
                prepend-inner-icon="mdi-email"
                type="email"
                required
              />
              <v-btn type="submit" color="primary" block>
                Subscribe
              </v-btn>
            </v-form>
          </v-col>
        </v-row>
      </v-container>


      


    </v-main>
  </v-app>
</template>


<script lang="ts" setup>

import { ref, computed } from 'vue';

const selectedCategory = ref<string | null>(null);

const categories = ['Movie', 'Book', 'Music'];

const filteredPosters = computed(() => {
  if (!selectedCategory.value) return posters;
  return posters.filter(p => p.category === selectedCategory.value);
});

const email = ref('');

const submitNewsletter = () => {
  if (email.value) {
    // Replace this with your actual newsletter logic (API call etc.)
    console.log('Subscribed with email:', email.value);
    alert(`Thanks for subscribing, ${email.value}!`);
    email.value = '';
  }
};



import grungeTexture from '@/assets/GrungePosterTextures01.png';
import AftersunPoster from '@/assets/Aftersun.png';
import DraculaPoster from '@/assets/Dracula.png';
import WhiplashPoster from '@/assets/Whiplash.png';
import EngravePoster from '@/assets/Engrave.png';


const posters = [
  {
    title: 'Aftersun',
    src: AftersunPoster,
    category: "Movie",
  },
  {
    title: 'Whiplash',
    src: WhiplashPoster,
    category: "Movie",
  },
  {
    title: 'Dracula',
    src: DraculaPoster,
    category: "Book",
  },
  {
    title: 'Engrave',
    src: EngravePoster,
    category: "Music"
  }
];

</script>


<style scoped>
.blend-image .v-img__img {
  mix-blend-mode: lighten;
  opacity: 0.3;
}



.v-card:hover {
  transform: scale(1.03);
  transition: transform 0.3s ease;
  z-index: 1;
}
</style>
