<template>
  <nav>
    <div class="container mx-auto p-5">
      <a href="/">
        <h1 class="text-gray-700 text-5xl"><i class="fa-solid fa-cat"></i> {{ title }}</h1>
      </a>
    </div>
  </nav>
</template>

<script>
export default {
  props: ['title']
}
</script> 