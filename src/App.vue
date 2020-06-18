<template>
  <div id="app">
<!--    <span class="icon-arrow-left2"></span>-->
<!--    <img src="./assets/logo.png">-->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  mounted: function () {
    console.log('mounted app')
  }
}
document.addEventListener('DOMContentLoaded', () => {
  // 设置网页文字上限大小
  const html = document.querySelector('html')
  let fontSize = window.innerWidth / 10
  fontSize = fontSize > 50 ? 50 : fontSize
  html.style.fontSize = fontSize + 'px'
})
</script>

<style>

</style>
