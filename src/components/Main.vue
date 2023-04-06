<template>
  <section class="wrapper">
    <List />
  </section>
</template>

<script>
import { ref } from 'vue' 
import List from '../components/List.vue'

export default { 
  name: "Main",
  components: {
    List
  },
  setup(props,ctx) {
    const count = ref(0)

    return {
      count
    }
  }
}
</script>

<style scoped lang="scss">
.wrapper {
    max-width: 1280px;
    margin: 0 auto;
  }
</style>
