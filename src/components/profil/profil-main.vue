<template>
<div class="profil-container">
    <h1 class="main-color">Персональная информация</h1>
    <div class="button-profil" v-if="!editActive" @click="openEdit" >Редактировать</div>
    <div class="form-box">
        <div class="flex" v-if="nameUser || editActive">
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
        <div class="flex" v-if="dateBirth ||editActive">
            <div class="label">Дата рожения:</div>
            <div class="info" v-if="!editActive ">{{dateBirth}}</div>
            <input v-if="editActive" type="date" class="input-form input-size" v-model="dateBirth"/>
        </div>
        <div class="flex" v-if="editActive || email">
            <div class="label">Почта:</div>
            <div class="info" v-if="!editActive">{{email}}</div>
            <input v-if="editActive" type="email" required class="input-form input-size" :class="{ 'error': emailError }" v-model="email"/>
        </div>
        <div class="flex" v-if="editActive || sity">
            <div class="label">Город:</div>
            <div class="info" v-if="!editActive">{{sity}}</div>
            <input v-if="editActive" type="text" class="input-form input-size" v-model="sity"/>
        </div>
        <div class="flex" v-if="editActive || numberTel">
            <div class="label">Телефон:</div>
            <div class="info" v-if="!editActive">{{numberTel}}</div>
            <input-telephone v-if="editActive" ref="telephone" :phone="phoneCopy" @getPhon="inputPhon($event)"/>
        </div>
        <div class="flex" v-if="editActive || languages.length">
            <div class="label">Языки:</div>
            <div class="box">
            <div class="info" v-if="!editActive || languages.length">
                
                <span v-for="item, i in languages" :key="i">{{i?", ":""}}{{item.title}}</span>
            </div>
            <select  v-if="editActive" class="input-form select-size" @change="updateSelect()" v-model="leng" size="1">
                <option v-for="item, id in titleLeng" :key="id" :value="item.val">{{item.title}}</option>
            </select>
            </div>
        </div>
        <div class="button-container" v-if="editActive">
            <div class="button-profil" @click="saveInfo">Сохранить</div> 
            <div class="button-profil" @click="сancel">Отмена</div>
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
            InputError:false,
            nameError: false,
            emailError: false,
            phoneCopy: null,
        }
    },
    watch: {
        nameUser(){
            this.nameUser = this.nameUser.replace(/[^a-zа-яё ]/gi, '');
        },
        email(){
            
        }
        
    },
    created(){
        if(localStorage){
            localStorage.nameUser?this.nameUser = localStorage.nameUser: null
            localStorage.dateBirth?this.dateBirth = localStorage.dateBirth: null
            localStorage.email?this.email = localStorage.email: null
            localStorage.sity?this.sity = localStorage.sity: null
            localStorage.numberTel?this.numberTel = localStorage.numberTel: null
            this.titleLeng.map(item=>{
                if(localStorage[item.val]) {
                    this.languages.push({
                        val: item.val,
                        title: localStorage[item.val]
                    })
                }
            })
            //localStorage.languages?this.languages = localStorage.languages: null
        }
    },
    computed: {
    },
    methods: {
        openEdit(){
            this.editActive = true;
            this.phoneCopy = this.numberTel;
        },
        сancel(){
            this.editActive = false;
             this.numberTel = this.phoneCopy;
        },

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
            console.log('1')
            this.InputError = false;
            this.nameUser.length < 3? 
                this.nameError = true: 
                this.nameError = false;
                /^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/.exec(this.email)? 
                this.emailError = false: 
                this.emailError = true;
                if(localStorage.sity){
                    localStorage.removeItem('sity')
                }
                this.titleLeng.map(item=>{
                    localStorage.removeItem(item.val)
                })
                
            if(!this.nameError && !this.emailError) {
                console.log('ww')
                localStorage.setItem('nameUser', this.nameUser);
                localStorage.setItem('dateBirth', this.dateBirth);
                localStorage.setItem('email', this.email);
                if(this.sity){
                    localStorage.setItem('sity', this.sity);
                }
                localStorage.setItem('numberTel', this.numberTel);
                if(this.languages.length){
                    this.languages.map(item=>{
                        localStorage.setItem(`${item.val}`, item.title)
                    });
                }
                //localStorage.setItem('languages', this.languages);
                this.editActive = false;
                this.phoneCopy = null;
            }
            else {
                this.InputError = true;
            }
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
    font-size: 30px;
    font-weight: 400;
    line-height: 24px;
    flex-direction: column;
    align-items: center;
}
.flex{
    margin: 10px;
    display: flex;
}
.box{
    max-width: 300px;
}
.label{
    min-width: 280px;
    text-align: end;
}
.info{
    min-width: 143px;
}

.main-color{
    color: #d5d5d5;
    font-size: 34px;
}

.select-size{
    width: 313px;
    font-size: 30px;
}
.button-container{
    margin: 20px;
    display: flex;
    justify-content: center;
}
@media (max-width: 720px) { 
    .flex{
        flex-direction: column;
        align-items: center;
    }
    .label{
        margin: 5px;
        text-align: center;
    }
    .info{
       text-align: center;
    }
}

</style>
<style lang="scss">
.error{
    border: 2px solid red !important;
}
.input-form{
    padding: 4px;
    outline:none;
    border-radius: 7px;
    background: #a5a5a5;
    border: 2px solid #333333;;
}
.input-size{
    width: 300px;
    font-size: 30px;
    height: 33px;
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
</style>