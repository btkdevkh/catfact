<template>
  <section class="random__fact" @click.self="closeModal">
    <div class="w-80 font-bold text-white bg-rose-500 text-center p-5 rounded fact" v-if="randomFact">
      <p>{{ randomFact.fact }}</p>
    </div>
  </section>
</template>

<script>
import { API_URL_FACT } from '../config'

export default {
  props: ['isOpen', 'delay'],
  data() {
    return {
      randomFact: null
    }
  },
  methods: {
    closeModal() {
      this.$emit('close')
    }
  },
  mounted() {
    fetch(API_URL_FACT)
      .then(res => res.json())
      .then(data => this.randomFact = data)
      .catch(err => console.log(err))
  }
}
</script>