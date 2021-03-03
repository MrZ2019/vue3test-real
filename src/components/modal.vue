<template>
<teleport to="#modal">
  <div id="center" v-if="isOpen">
    <h2><slot>this is a modal {{msg}}</slot></h2>
    <button @click="buttonClick">Close</button>
  </div>
</teleport>
</template>
<script lang="ts">
import { defineComponent,ref } from 'vue'
export default defineComponent({
  props: ['isOpen'],
  emits: {
    'close-modal': null
  },
  setup(props, context) {
    const buttonClick = () => {
      context.emit('close-modal')
    }
    const msg = ref("apple")
    return {
      buttonClick,
      msg,
    }
  }
})
</script>
