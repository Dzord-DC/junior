<template>
  <div class="container" id="main">
    <avatar-main />
    <profil-main />
    <password-main />
  </div>
</template>

<script>
import AvatarMain from './components/avatar/avatar-main.vue'
import PasswordMain from './components/password/password-main.vue'
import ProfilMain from './components/profil/profil-main.vue'

export default {
  name: 'App',
  components: {
    AvatarMain,
    ProfilMain,
    PasswordMain
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
  width: 100%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  background-color: #333333;
  flex-direction: column;
  align-items: center;
}
</style>
