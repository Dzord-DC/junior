<template>
    <div class="input_box" @click="delitedAvatar()">
        <div class="input-file">
          <div class="icons" >&#10060;</div>
        </div>
    </div>
</template>

<script>
export default {
  name: "avatarDelited",
  data(){
    return {}
  },
  methods: {
    delitedAvatar() {
     localStorage.removeItem('avatar');
     this.$emit('updateAvatar');
  }
}
}
</script>

<style scoped>
.input_box{
  background-color: rgba(238, 230, 230, 0.5);
  width: 40px;
  height: 40px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
}
.input_box:hover{
  background-color: rgba(238, 230, 230, 0.8);
}
.edit-avatar{
  display: none;
}
.icons{
    cursor: pointer;
    width: 33px;
    height: 35px;
    font-size: 25px;
}
</style>