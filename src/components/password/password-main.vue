<template>
<div class="password-container">
  <div class="button-profil" @click="openForm">Сменить пароль</div>
  <div v-if="formShow" class="modal-container">
    <div class="modal-forma" >
        <div>
        <div class="label">Текущий пароль</div>
        <input type="password" required class="input-form input-size" :class="{ 'error': oldPasswordEr }" v-model="oldPassword">
        <div class="label">Новый пароль</div>
        <div v-if="newPasswordEr" class="error-label">Пароль должен быть от 6 до 20 символов, содержать цифры, прописные и строчные буквы, а также специальные символы</div>
        <input type="password" required class="input-form input-size" :class="{ 'error': newPasswordEr }" v-model="newPassword">
        <div class="label">Подтверждение пароля</div>
        <div v-if="checkPasswordEr" class="error-label">Ошибка подтверждения пароля</div>
        <input type="password" required class="input-form input-size" :class="{ 'error': checkPasswordEr }" v-model="checkPassword">
        </div>
        <div class="button-container" >
            <div class="button-profil" @click="save">Сохранить</div> 
            <div class="button-profil" @click="clearData">Отмена</div>
        </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
    name: "passwordMain",
    data(){
        return {
            formShow: false,
            oldPassword: null,
            newPassword: null,
            checkPassword: null,
            oldPasswordEr: false,
            newPasswordEr: false,
            checkPasswordEr: false,
            fault:false,
            main:null,
        }
    },
    methods: {
        clearData(){
            this.oldPasswordEr = false;
            this.newPasswordEr = false;
            this.checkPasswordEr = false;
            this.newPassword = null;
            this.oldPassword = null;
            this.checkPassword = null;
            this.formShow = false;
            if(this.main) {
                this.main.classList.remove('no-scroll');
            }
        },
        openForm(){
            this.formShow=true;
            this.main = document.getElementById('main');
            this.main.classList.add('no-scroll');
        },
        save(){
            this.oldPasswordEr = false;
            this.newPasswordEr = false;
            this.checkPasswordEr = false;
            if(!this.oldPassword){
                this.oldPasswordEr = true;
            } 
            if(!/((?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[\W]).{6,20})/.exec(this.newPassword)){
                this.newPasswordEr = true;
            }
            if(!this.checkPassword){
                this.checkPasswordEr = true;
            }
            if(!this.checkPasswordEr && !this.newPasswordEr && !this.oldPasswordEr){
                if(this.newPassword != this.checkPassword){
                    this.checkPasswordEr = true;
                } else {
                    this.clearData();
                }
            
            }
        },
        
    }
}
</script>

<style lang="scss" scoped>
.modal-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background-color: rgba(207, 207, 207, 0.3);
    display: flex;
    align-items: center;
    justify-content: center;
}
.password-container{
    font-size: 30px;
    color: #cfcfcf;
}
.modal-forma{
    display: flex;
    width: 400px;
    padding: 10px;
    background-color: #333333;
    border: 2px solid #cfcfcf;
    border-radius: 5px;
    flex-direction: column;
}
.error-label{
    color: #eb6935;
    font-size: 12px;
}
</style>
<style lang="scss">
.no-scroll{
    position: fixed;
    overflow: hidden;
}
</style>