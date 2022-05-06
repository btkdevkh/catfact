<template>
  <div class="relative rounded overflow-hidden cursor-pointer hover:text-white">
    <i class="text-3xl absolute right-2 top-2 fa-solid fa-cat"></i>
    <router-link :to="{ name: 'Details', params: { breed: breed.breed } }">
      <img :src="foundCatPic && foundCatPic.path ? foundCatPic.path : catgeneric" class="w-full h-52 object-cover" />
    </router-link>
    <div class="flex flex-col justify-center text-gray-600 bg-white p-5 shadow-md h-60 hover:bg-green-900 hover:shadow-inner hover:text-white transition ease-in-out delay-100" @click="toggleModal">
      <p class="mb-2"><strong>Race:</strong> {{ breed.breed }}</p>
      <p class="mb-2"><strong>Pilosité:</strong> {{ breed.coat ? breed.coat : 'N/A' }}</p>
      <p class="mb-2"><strong>Pays:</strong> {{ breed.country ? breed.country : 'N/A' }}</p>
      <p class="mb-2"><strong>Originaire:</strong> {{ breed.origin }}</p>
        <p><strong>Motif:</strong> {{ breed.pattern ? breed.pattern : 'N/A' }}</p>
    </div>
  </div>
</template>

<script>
import catgeneric from '../assets/img/cats/catgeneric.jpg'
import { catPics } from '../data/catPics'

export default {
  props: ['breed', 'toggleModal'],
  data() {
    return {
      catgeneric,
      catPics,
    }
  },

  computed: {
    foundCatPic() {
      return catPics.find(c => c.breed.toLowerCase() === this.breed.breed.toLowerCase())
    }
  }
}
</script>