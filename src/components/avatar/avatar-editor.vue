<template>
  <div class="row">
    <div class="input_box">
        <label for="inputAvatar" class="input-file">
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
  background-color: rgba(238, 230, 230, 0.5);
  width: 40px;
  height: 40px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
}
.input-file:hover{
  background-color: rgba(238, 230, 230, 0.8);
}
.edit-avatar{
  display: none;
}
.icons{
  cursor: pointer;
  width: 23px;
  height: 36px;
  font-size: 25px;
  transform: rotate(90deg);
}

</style>