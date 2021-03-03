<template>

  <Suspense>
  <template #default>
    <async-show />
  </template>
  <template #fallback>
    <h1>Loading !...</h1>
  </template>
  </Suspense>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/ -->

  <button @click="openModal">Open Modal</button><br/>
  <h1>x=:{{x}}</h1>
  <modal :isOpen="modalIsOpen" @close-modal="onModalClose"></modal>

  <img :src="result[0].url" alt="">
</template>

<script lang='ts'>
// import HelloWorld from './components/HelloWorld.vue'
import { defineComponent, ref } from 'vue'
import modal from './components/modal.vue'
import asyncShow from './components/asyncShow.vue'
import useMousePosition from './components/useMousePosition.vue'
import useURLLoader from './components/useURLLoader.vue'

// 在应用中的使用，可以定义不同的数据类型
interface DogResult {
  message: string;
  status: string;
}
interface CatResult {
  id: string;
  url: string;
  width: number;
  height: number;
}

export default defineComponent({
  props: {
    isOpen: Boolean,
  },
  emits: {
    'close-modal': null
  },
  components: {modal, asyncShow},
  setup(props, context) {

    const { x, y } = useMousePosition()
    // const { result } = useUrlLoader('https://dog.ceo/api/breeds/image/random')
    const { result } = useURLLoader<CatResult[]>('https://api.thecatapi.com/v1/images/search?limit=1')

    let a:CatResult = <CatResult>result[0];
    

    const buttonClick = () => {
      context.emit('close-modal')
    }
    const modalIsOpen = ref(false)

    const openModal = () => {
      modalIsOpen.value = true
    }
    const onModalClose = () => {
      modalIsOpen.value = false
    }
    return {
      buttonClick,
      modalIsOpen,
      openModal,
      onModalClose,
      x,y,
      result,
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
