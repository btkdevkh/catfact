<template>
  <BreedList :breeds='breeds' :toggleModal="toggleModal" />
  <BreedPagination :links="links" @change="handleChangeUrl" />
  <teleport to=".modals" v-if="isOpen">
    <Modal :isOpen="isOpen" @close="toggleModal" />
  </teleport>
</template>

<script>
import { ref, onMounted } from 'vue'
import BreedList from '../components/BreedList.vue'
import BreedPagination from '../components/BreedPagination.vue'
import Modal from '../components/Modal.vue'
import { API_URL } from '../config'

export default {
  name: 'Home',
  components: { BreedList, BreedPagination, Modal },
  setup () {
    const breeds = ref([]);
    const links = ref([]);
    const isOpen = ref(false);
    const inc = ref(1);

    const toggleModal = () => {
      isOpen.value = !isOpen.value
    };

    const handleChangeUrl = (link) => {
      link.active = !link.active 
      if(link.label === '<') {
        inc.value--
        link.url = `${API_URL}?page=${inc.value}`
      }

      if(link.label === '>') {
        inc.value++
      } else {
        inc.value = link.url.split('')[link.url.split('').length - 1]
      }

      const linkLengthWithoutPrevAndNextBtns = links.value.length - 2;
      if(inc.value <= 0) inc.value = 1
      if(inc.value >= linkLengthWithoutPrevAndNextBtns) inc.value = linkLengthWithoutPrevAndNextBtns

      link.url = `${API_URL}?page=${inc.value}`

      fetch(link.url)
        .then(res => res.json())
        .then(datas => {
          breeds.value = datas.data
        })
        .catch(err => console.log(err))
    };

    onMounted(() => {
      fetch(API_URL)
        .then(res => res.json())
        .then(datas => {
          breeds.value = datas.data
          links.value = datas.links
        })
        .catch(err => console.log(err))
    })

    return { breeds, links, isOpen, toggleModal, handleChangeUrl }
  }
}
</script>
