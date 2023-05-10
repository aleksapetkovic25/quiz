<template>
    <div class="game-info">
        <img :src="'/src/assets/'+rival.img" alt="tragac">
        <div class="info">
            <p>Name: {{rival.name}}</p>
            <p>Level: {{level.name}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['level', 'rival'],
    data(){
        return{

        }
    },

}
</script>

<style lang="scss" scoped>
.game-info{
    display: flex;
    width: max-content;
    padding: 10px 25px 10px 15px;
    height: 100px;
    background-color:#585858 ;
    
    img{
        margin-right: 10px;
    }

    .info{
        color: #fff;
        margin: auto;
        text-transform: capitalize;
    }
}
</style>