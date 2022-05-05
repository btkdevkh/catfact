<template>
  <Navbar :title="title" />
  <main class="container mx-auto p-5">
    <BreedList :breeds='breeds' :toggleModal="toggleModal" />
    <BreedPagination :links="links" @change="handleChangeUrl" />
  </main>

  <teleport to=".modals" v-if="isOpen">
    <Modal :isOpen="isOpen" @close="toggleModal" />
  </teleport>
</template>

<script>
import Navbar from './components/Navbar.vue'
import BreedList from './components/BreedList.vue'
import Modal from './components/Modal.vue'
import BreedPagination from './components/BreedPagination.vue'
import { API_URL } from './config'

export default {
  name: 'App',
  components: { Navbar, BreedList, Modal, BreedPagination },
  data() {
    return {
      title: 'Cat Ninja',
      breeds: [],
      links: [],
      isOpen: false,
      inc: 1,
    }
  },

  methods: {
    toggleModal() {
      this.isOpen = !this.isOpen
    },

    handleChangeUrl(link) {
      link.active = !link.active 
      if(link.label === '<') {
        this.inc--
        link.url = `${API_URL}?page=${this.inc}`
      }

      if(link.label === '>') {
        this.inc++
      } else {
        this.inc = link.url.split('')[link.url.split('').length - 1]
      }

      const linkLengthWithoutPrevAndNextBtns = this.links.length - 2;
      if(this.inc <= 0) this.inc = 1
      if(this.inc >= linkLengthWithoutPrevAndNextBtns) this.inc = linkLengthWithoutPrevAndNextBtns

      link.url = `${API_URL}?page=${this.inc}`

      fetch(link.url)
        .then(res => res.json())
        .then(datas => {
          this.breeds = datas.data
        })
        .catch(err => console.log(err))
    }
  },

  mounted() {
    fetch(API_URL)
      .then(res => res.json())
      .then(datas => {
        this.breeds = datas.data
        this.links = datas.links
      })
      .catch(err => console.log(err))
  }

  // mounted() { console.log('mounted') },
  // updated() { console.log('updated') },
  // unmounted() { console.log('unmounted') }
}
</script>