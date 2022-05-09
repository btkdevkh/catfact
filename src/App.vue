<template>
  <Navbar :title="title" />
  <main class="container mx-auto p-5">
    <NavigationButton />
    <router-view />
  </main>
</template>

<script>
import Navbar from './components/Navbar.vue'
import NavigationButton from './components/NavigationButton.vue'

export default {
  name: 'App',
  components: { Navbar, NavigationButton },
   data() {
    return {
      title: 'CAT NINJA',
    }
  }
}
</script>