<script lang='ts'>
import { ref, onMounted, onUnmounted } from 'vue'
function useMouseTracker() {
  // const positions = reactive<MousePostion>({
  //   x: 0,
  //   y: 0
  // })
  const x = ref(0)
  const y = ref(0)
  const updatePosition = (event:any) => {
    x.value = event.clientX
    y.value = event.clientY
  }
  onMounted(() => {
    document.addEventListener('mousemove', updatePosition)
  })
  onUnmounted(() => {
    document.removeEventListener('click', updatePosition)
  })
  return { x, y }
}
export default useMouseTracker
</script>
