<template>
  <div class="home">
    <div class="container">
      <div class="image-title">
        <img alt="Vue logo" src="../assets/logo.png">
        <HelloWorld msg="АПК – Звонок"/>
      </div>
      <div class="title">
        <ControlBlock/>
        <FooterRef/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import ControlBlock from '@/components/ControlBlock.vue'
import FooterRef from '@/components/FooterRef.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    FooterRef,
    ControlBlock
  }
}
</script>

<style scoped>
.title {
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
