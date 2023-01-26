<template>
    <div class="avtar-containet">
        <img :src="avatarSRC" alt="" class="avatar" >
        <avatar-deleted @updateAvatar="update" class="deleted-avatar_position item-hiden"/>
        <avatar-editor @updateAvatar="update" class="editor-avatar_position item-hiden"/>
    </div>
</template>

<script>
import avatarDeleted from './avatar-deleted.vue'
import avatarEditor from './avatar-editor.vue'
export default {
  components: { avatarEditor,avatarDeleted },
    data(){
        return {
            avatarSRC: null,
        }
    },
    created(){
        this.avatarSRC = localStorage.avatar?localStorage.avatar:require('@/assets/default.png');
    },
    methods:{
        update(){
            if(localStorage.avatar){
                this.avatarSRC= localStorage.avatar
            } else {
                this.avatarSRC=require('@/assets/default.png');
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.avtar-containet{
    position: relative;
}
.avatar{
    width: 225px;
    height: 310px;
    border-radius: 50px;
    object-fit: cover;
}
.avtar-containet:hover > .item-hiden{
        opacity: 1;
    }
.deleted-avatar_position{
    position: absolute;
    top: 10px;
    right: 20px;
}
.editor-avatar_position{
    position: absolute;
    bottom: 20px;
    right: 20px;
}
.item-hiden{
    opacity: 0;
    transition: 0.3s;
}
</style>