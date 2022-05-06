<template>
  <Navbar :title="title" />
  <main class="container mx-auto p-5">

    <div class="mb-5 flex gap-2 justify-center">
      <button @click="redirect" class="bg-green-900 text-white px-5 py-2 rounded">Home</button>
      <button @click="back" class="bg-green-900 text-white px-5 py-2 rounded">Go Back</button>
      <button @click="forward" class="bg-green-900 text-white px-5 py-2 rounded">Go Forward</button>
    </div>

    <router-view />
  </main>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: { Navbar },
   data() {
    return {
      title: 'Cat Ninja',
    }
  },
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

  // mounted() { console.log('mounted') },
  // updated() { console.log('updated') },
  // unmounted() { console.log('unmounted') }
}
</script>