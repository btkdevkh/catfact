<template>
  <section class="mb-8 breed__list">
    <div class="grid md:grid-cols-3 lg:grid-cols-4 gap-4 breed__grid">
      <BreedCard 
        v-for="breed in breeds" 
        :key="breed.breed"
        :breed="breed" 
        :toggleModal="toggleModal" 
      />
    </div>
  </section>
</template>

<script>
import BreedCard from './BreedCard.vue'

export default {
  props: ['breeds', 'toggleModal'],
  components: { BreedCard },
}
</script>
