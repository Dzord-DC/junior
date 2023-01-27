<template>
<div class="profil-container">
    <h1 class="main-color">Персональная информация</h1>
    <div class="button-profil" v-if="!editActive" @click="editActive=true" >Редактировать</div>
    <div class="form-box">
        <div class="flex" v-if="editActive">
            <div class="label">Имя:</div>
            <div class="info" v-if="!editActive">{{nameUser}}</div>
            <input 
                v-if="editActive" 
                type="text" required 
                class="input-form input-size" 
                v-model="nameUser"
                :class="{ 'error': nameError }"
            />
        </div>
        <div class="flex" v-if="editActive">
            <div class="label">Дата рожения:</div>
            <div class="info" v-if="!editActive">{{dateBirth}}</div>
            <input v-if="editActive" type="date" class="input-form input-size" v-model="dateBirth"/>
        </div>
        <div class="flex" v-if="editActive">
            <div class="label">Почта:</div>
            <div class="info" v-if="!editActive">{{email}}</div>
            <input v-if="editActive" type="email" required class="input-form input-size" :class="{ 'error': emailError }" v-model="email"/>
        </div>
        <div class="flex" v-if="editActive">
            <div class="label">Город:</div>
            <div class="info" v-if="!editActive">{{sity}}</div>
            <input v-if="editActive" type="text" class="input-form input-size" v-model="sity"/>
        </div>
        <div class="flex" v-if="editActive">
            <div class="label">Телефон:</div>
            <div class="info" v-if="!editActive">{{numberTel}}</div>
            <input-telephone v-if="editActive" @getPhon="inputPhon($event)"/>
        </div>
        <div class="flex" v-if="editActive">
            <div class="label">Языки:</div>
            <div class="info" v-if="!editActive || languages.length">
                <span v-for="item, i in languages" :key="i">{{i?", ":""}}{{item.title}}</span>
            </div>
            <select  v-if="editActive" class="input-form input-size" @change="updateSelect()" v-model="leng" size="1">
                <option v-for="item, id in titleLeng" :key="id" :value="item.val">{{item.title}}</option>
            </select>
        </div>
        <div v-if="editActive">
            <div class="button-profil" @click="saveInfo">Сохранить</div> 
            <div class="button-profil" @click="editActive=false">Отмена</div>
        </div>
        </div>
</div>
  

</template>

<script>
import inputTelephone from './input-telephone.vue';
export default {
  components: { inputTelephone },
    name:"profilMain",
    data(){
        return {
            editActive: false,
            nameUser: '',
            dateBirth: null,
            email: null,
            sity:null,
            numberTel: null,
            languages: [],
            titleLeng:[
                {val:'rus', title: 'Русский'},
                {val:'eng', title: 'Английский'},
                {val:'spa', title: 'Испанский'},
                {val:'port', title: 'Португальский'},
            ],
            leng: null,
        }
    },
    watch: {
        nameUser(){
            this.nameUser = this.nameUser.replace(/[^a-zа-яё ]/gi, '');
        },
        email(){
            
        }
        
    },
    computed: {
        nameError(){
            return this.nameUser.length < 3;
        },
        emailError(){
            return /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/.exec(this.email)
        }
    },
    methods: {
        inputPhon(phone){
            this.numberTel = phone;
        },
        updateSelect() {
            let cod = this.languages.findIndex((item)=>{
                return item.val == this.leng
            });
            if(cod == -1){
                this.languages.push(this.titleLeng.find(item=>item.val == this.leng))
            } else {
                this.languages.splice(cod, 1);
            }
            this.leng = null;
        },
        saveInfo() {
            let data = {
                nameUser: this.nameUser,
                dateBirth: this.dateBirth,
                email: this.email,
                sity:this.sity,
                numberTel: this.numberTel,
                languages: this.languages,
            }
            localStorage.setItem('userInfo', data);
        }
    }


}
</script>

<style lang="scss" scoped>
.profil-container{
    display: flex;
    color: #cfcfcf;
    display: flex;
    flex-wrap: wrap;
    font-size: 14px;
    font-weight: 400;
    line-height: 24px;
    flex-direction: column;
    align-items: center;
}
.button-profil{
    background: #363636;
    border: 1px solid #363636;
    border-radius: 3px;
    margin-bottom: 20px;
    margin-right: 20px;
    padding: 6px 24px;
    color: #a5a5a5;
    cursor: pointer;
    transition: 0.3s;
}
.button-profil:hover{
     background: #272727;
     color: #cfcfcf;
      border: 1px solid  #a5a5a5;
}
.main-color{
    color: #d5d5d5;
    font-size: 34px;
}
.error{
    border: 2px solid red !important;
}
.input-size{
    width: 300px;
    padding: 4px;
}

</style>
<style lang="scss">
.input-form{
    outline:none;
    border-radius: 7px;
    font-size: 20px;
    background: #a5a5a5;
    border: none;
}
</style>