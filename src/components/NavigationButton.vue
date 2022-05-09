<template>
  <div class="mb-10 flex gap-2 justify-center">
    <button @click="back" class="bg-blue-700 text-white px-5 py-2 rounded">Précédent</button>
    <button @click="redirect" class="bg-blue-700 text-white px-5 py-2 rounded">Accueil</button>
    <button @click="forward" class="bg-blue-700 text-white px-5 py-2 rounded">Suivant</button>
  </div>
</template>

<script>
export default {
  methods: {
    redirect() {
      this.$router.push({ name: 'Home' })
    },
    back() {
      this.$router.go(-1)
    },
    forward() {
      this.$router.go(1)
    }
  }
}
</script>