<template>
  <div class="container">
    <avatar-main />
    <profil-main />
  </div>
</template>

<script>
import AvatarMain from './components/avatar/avatar-main.vue'
import ProfilMain from './components/profil/profil-main.vue'

export default {
  name: 'App',
  components: {
    AvatarMain,
    ProfilMain
  }
}
</script>

<style>
#app {
  font-family: monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.container{
  margin: 0 auto;
  padding: 50px;
  display: flex;
  justify-content: center;
  background-color: #333333;
  flex-direction: column;
  align-items: center;
}
</style>
