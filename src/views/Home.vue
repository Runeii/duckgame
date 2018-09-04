<template>
  <div class="home" @click="start">
    <img alt="Vue logo" src="../assets/duck.0.png">
    <p>Tap to begin</p>
  </div>
</template>

<script>
export default {
  name: 'home',
  methods: {
    start () {
      this.$router.push({ path: '/game' })
    }
  }
}
</script>
