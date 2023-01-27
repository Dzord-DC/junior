<template>
<div>
    <select  class="code" @change="updateSelect()" v-model="code" size="1">
                <option v-for="item, id in codeConty" :key="id" :value="item.val">{{item.title}}</option>
            </select>
    <input type="text" class="input-form" :placeholder="imputCode.mask" v-model="telefone" />
</div>
  
</template>

<script>
export default {
    name:"inputPelephone",
    props: {
        volueTel:Number
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
            telefone: null,
        }
    },
    watch: {
        telefone(){
            this.telefone = this.telefone.replace(/[a-zа-яё]/gi, '');
            if(this.telefone.length > this.imputCode.mask.length){
                this.telefone = this.telefone.slice(0, this.imputCode.mask.length);
            }
            for(let i=0; i<this.telefone.length; i++){
                if(this.imputCode.mask[i]!="9" && this.telefone[i]!=this.imputCode.mask[i]){
                    this.telefone=this.telefone.slice(0,i)+this.imputCode.mask[i]+this.telefone.slice(i) 
                }
            }
            this.$emit("getPhon", this.telefone)
        }
    },
    methods: {
        updateSelect(){
                this.imputCode = this.codeConty.find(item=>item.val == this.code);
                this.telefone = "";
            }
    },
    mounted(){
        this.updateSelect()
    }
        
}

</script>

<style>

</style>