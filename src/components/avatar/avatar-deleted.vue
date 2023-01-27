<template>
    <div class="input_box" @click="delitedAvatar()">
        <div class="input-label">Удалить</div>
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
  cursor: pointer;
  background-color: rgba(238, 230, 230, 0.5);
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
}
.input_box:hover{
  background-color: rgba(238, 230, 230, 0.8);
}
.input_box:hover >.input-label{
  width: 95px;
}
.edit-avatar{
  display: none;
}
.icons{ 
    width: 36px;
    height: 36px;
    font-size: 25px;
    padding: 2px;
}
.input-label{
  width: 0;
  overflow: hidden;
  height: 40px;
  transition: 0.5s;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>