<template>
  <section class="random__fact" @click.self="closeModal">
    <div class="w-80 font-bold text-white bg-rose-500 text-center p-5 rounded fact" v-if="randomFact">
      <p>{{ randomFact.fact }}</p>
    </div>
  </section>
</template>

<script>
import { ref } from '@vue/reactivity'
import { API_URL_FACT } from '../config'
import { watchEffect } from '@vue/runtime-core'

export default {
  props: ['isOpen', 'delay'],
  setup (props, context) {
    const randomFact = ref(null)

    const closeModal = () => {
      context.emit('close')
    }

    watchEffect(() => {
      fetch(API_URL_FACT)
        .then(res => res.json())
        .then(data => randomFact.value = data)
        .catch(err => console.log(err))
    })

    return { randomFact, closeModal }
  }
}
</script>
