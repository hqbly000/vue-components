<template>
  <div>
    <p :key="item" v-for="item in list">{{ item }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: ['a', 'b']
    }
  }
}
</script>

<style></style>
