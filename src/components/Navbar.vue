<template>
  <nav>
    <div class="container mx-auto p-5 flex justify-between items-center">
      <router-link :to="{ name: 'Home' }">
        <h1 class="text-gray-700 text-5xl">
          <i class="fa-solid fa-cat"></i> {{ title }}
        </h1>
      </router-link>
      <router-link :to="{ name: 'About' }" class="text-gray-700 text-2xl uppercase">About</router-link>
    </div>
  </nav>
</template>

<script>
export default {
  props: ['title']
}
</script> 