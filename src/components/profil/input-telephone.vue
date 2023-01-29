<template>
<div>
    <select  class="code input-form input-form_select input-form_font" @change="updateSelect()" v-model="code" size="1">
                <option v-for="item, id in codeConty" :key="id" :value="item.val">{{item.title}}</option>
            </select>
    <input type="text" class="input-form input-form_size input-form_margin input-form_font" :placeholder="imputCode.mask" v-model="telephone" />
</div>
  
</template>

<script>
import { nextTick } from '@vue/runtime-core';
export default {
    name:"inputPelephone",
    props: {
        phone:String
    },
    data(){
        return{
            codeConty: [
                {val:7, title:"+7", mask:'(999)999-99-99'},
                {val:1, title:"+1", mask:'(999)999-9999'},
                {val:52, title:"+52", mask:'-99-999 99 99'},
                {val:55, title:"+55", mask:'–9999999'},
            ],
            code:7,
            imputCode:{},
            telephone: null,
        }
    },
    watch: {
        telephone(){
            this.telephone = this.telephone.replace(/[a-zа-яё]/gi, '');
            if(this.telephone.length > this.imputCode.mask.length){
                this.telephone = this.telephone.slice(0, this.imputCode.mask.length);
            }
            for(let i=0; i<this.telephone.length; i++){
                if(this.imputCode.mask[i]!="9" && this.telephone[i]!=this.imputCode.mask[i]){
                    this.telephone=this.telephone.slice(0,i)+this.imputCode.mask[i]+this.telephone.slice(i) 
                }
            }
            this.$emit("getPhon", `+${this.code} ${this.telephone}`)
        }
    },
    methods: {
        updateSelect(){
                this.imputCode = this.codeConty.find(item=>item.val == this.code);
                this.telephone = "";
            },
        getPhoneEdit(){
            if(this.phone){
                let srtag = this.phone.split(" ");
                console.log('dwadaw', srtag);
                nextTick(()=>{
                    this.code = srtag[0].replace(/[^0-9]/gi, '');
                    this.telephone = srtag[1];
                });
            }
        },
    },
    mounted(){
        this.getPhoneEdit();
        this.updateSelect();
    }
        
}

</script>

<style lang="scss" scoped>
.input-form_margin{
    margin-left: 5px;
}
.input-form_font{
    font-size: 30px;
    height: 33px;
}
.input-form_select{
     padding: 3px;
     height: 45px;
}
.input-form_size{
    width: 213px;
}

</style>