<template>
<div class="profil-container">
    <h1 class="main-color">Персональная информация</h1>
    <div class="button-profil">Редактировать</div>
</div>
  

</template>

<script>
export default {
    name:"profilMain"

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
</style>