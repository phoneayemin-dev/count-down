<script>
import CountDown from "../src/components/CountDown.vue"
export default {
  components: {
    CountDown
  }
}
</script>
<template>
  <main class="main-section">
    <CountDown />
  </main>
</template>

<style>
.main-section {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 0 0 50%;
}
</style>
