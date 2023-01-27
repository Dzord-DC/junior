<template>
  <div class="row">
    <div class="input_box">
        <label for="inputAvatar" class="input-file">
          <div class="input-label">Редактировать</div>
          <div class="icons" >&#9998;</div>
            <input 
              type="file" 
              class="edit-avatar"
              id="inputAvatar" 
              ref="inputAvatar" 
              @change="loadAva()" 
              accept=".jpg, .jpeg, .png">
              
        </label>
    </div>
    </div>
</template>

<script>
export default {
  name: "AvatarEditor",
  data(){
    return {
      file: ''
    }
  },
  methods: {
    loadAva() {
      this.file = this.$refs.inputAvatar.files[0]
      let reader = new FileReader();
      reader.onloadend = ()=> {
        localStorage.setItem('avatar', reader.result);
        this.$emit('updateAvatar');
      }
      reader.readAsDataURL(this.file);
    },
  }
}
</script>

<style scoped>
.input-file{
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
  background-color: rgba(238, 230, 230, 0.5);
  border-radius: 20px;
  cursor: pointer;
}
.input-file:hover{
  background-color: rgba(238, 230, 230, 0.8);
  
}
.input-file:hover >.input-label{
  width: 105px;
}
.edit-avatar{
  display: none;
}
.icons{
    width: 30px;
    height: 30px;
    border-radius: 20px;
    font-size: 25px;
    transform: translate(3px, 3px) rotate(90deg);
    padding: 6px;
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