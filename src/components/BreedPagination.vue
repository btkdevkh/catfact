<template>
  <div class="bleed__btns text-center">
    <button 
      class="btn" 
      :class="link.active ? 'active' : ''"
      v-for="link in links" 
      :key="link.label"
      @click="change(link)"
      ref="btn"
    >
      {{ 
        link.label === 'Previous' ? 
        link.label = '<' : 
        link.label === 'Next' ? 
        link.label = '>' : 
        link.label
      }}
    </button>
  </div>
</template>

<script>
export default {
  props: ['links'],
  setup (props, context) {
    const change = (link) => {
      props.links.forEach(el => el.active = false)
      context.emit('change', link)
    }

    return { change }
  }
}
</script>
