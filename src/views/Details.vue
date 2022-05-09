<template>
  <div class="relative rounded overflow-hidden md:w-1/2 w-80 mx-auto" v-if="breedDetails">
    <i class="text-3xl absolute right-2 top-2 fa-solid fa-cat"></i>
    <img :src="foundCatPic && foundCatPic.path ? foundCatPic.path : catgeneric" class="w-full h-52 object-cover" />
    <div class="flex flex-col justify-center text-gray-600 bg-white p-5 shadow-md h-60">
      <p class="mb-2"><strong>Race:</strong> {{ breedDetails.breed }}</p>
      <p class="mb-2"><strong>Pilosité:</strong> {{ breedDetails.coat ? breedDetails.coat : 'N/A' }}</p>
      <p class="mb-2"><strong>Pays:</strong> {{ breedDetails.country ? breedDetails.country : 'N/A' }}</p>
      <p class="mb-2"><strong>Originaire:</strong> {{ breedDetails.origin }}</p>
      <p><strong>Motif:</strong> {{ breedDetails.pattern ? breedDetails.pattern : 'N/A' }}</p>
    </div>
  </div>
</template>

<script>
import { API_URL } from '../config'
import { catPics } from '../data/catPics'
import catgeneric from '../assets/img/cats/catgeneric.jpg'

export default {
  props: ['breed'],
  data() {
    return {
      breeds: [],
      breedDetails: null,
      catgeneric,
      catPics,
    }
  },

  methods: {
    async getAllBreeds() {
      const res1 = await fetch(API_URL)
      const data1 = await res1.json()
      const res2 = await fetch(`${API_URL}?page=2`)
      const data2 = await res2.json()
      const res3 = await fetch(`${API_URL}?page=3`)
      const data3 = await res3.json()
      const res4 = await fetch(`${API_URL}?page=4`)
      const data4 = await res4.json()

      this.breeds = [...data1.data, ...data2.data, ...data3.data, ...data4.data]

      this.breedDetails = this.breeds.find(b => {
        return b.breed.toLowerCase() === this.breed.toLowerCase()
      })
    }
  },

  mounted() {
    this.getAllBreeds()    
  },

  computed: {
    foundCatPic() {
      if(this.breedDetails) return catPics.find(c => c.breed.toLowerCase() === this.breedDetails.breed.toLowerCase())
    }
  }
}
</script>