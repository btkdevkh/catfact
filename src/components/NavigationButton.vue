<template>
  <div class="mb-10 flex gap-2 justify-center">
    <button @click="back" class="bg-blue-700 text-white px-5 py-2 rounded">Précédent</button>
    <button @click="redirect" class="bg-blue-700 text-white px-5 py-2 rounded">Accueil</button>
    <button @click="forward" class="bg-blue-700 text-white px-5 py-2 rounded">Suivant</button>
  </div>
</template>

<script>
import { useRouter } from 'vue-router'

export default {
  setup () {
    const router = useRouter()

    const redirect = () => {
      router.push({ name: 'Home' })
    }

    const back = () => {
      router.go(-1)
    }
    
    const forward = () => {
      router.go(1)
    }

    return { redirect, back, forward }
  }
}
</script>
