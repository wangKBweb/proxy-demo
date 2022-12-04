<script setup>
import { ref } from 'vue'

const count = ref(0)

const a = 1

// const p = new Proxy(a, {
//   get(obj, prop) {
//     console.log(obj, prop, '我是a');
//     return obj
//   }
// })

const btnClick = () => {
  count.value++
  console.log(a);
}

</script>

<template>
  <div class="card">
    <button type="button" @click="btnClick">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
