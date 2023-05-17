<template>
    <div class="wrapper rivals" :class="{hide: selectedRival, 'rotate-out': rotateRivals}">
        <div class="rival" v-for="(rival, index) in rivals" :key="index" @click="selectRival(rival)">
            <img :src="'/src/assets/' + rival.img" alt="avatar">
            <div class="overlay">
                <p>{{rival.name}}</p>
            </div>
        </div>
    </div>
</template>




<script>
export default {
    props: ['rivals'],
    data(){
        return{
            selectedRival: null,
            rotateRivals: false
        }
    },
    methods: {
        selectRival(rival){
            this.rotateRivals = true;
            this.$emit('selectedRival', rival)

            setTimeout(() => {
                this.selectedRival = rival;
            }, 300);
        }
    }
}
</script>





<style lang="scss" scoped>
$borderRadius: 20px;

.rivals{

    &.hide{
        display: none;
    }

    display: flex;
    justify-content: space-between;

    .rival{
        position: relative;
        width: 30%;
        border-radius: $borderRadius;
        box-shadow: 0px 0px 8px 1px rgba(71,71,71,0.93);
        background-color: rgb(39, 39, 39);

        .overlay{
            position: absolute;
            border-radius: $borderRadius;
            display: flex;
            visibility: hidden;
            justify-content: center;
            align-items: center;

            p{
                transform: translateY(120px);
                transition: transform 1s ease;
                color: #fff;
                text-transform: uppercase;
                font-weight: 700;
                letter-spacing: 5px;
            }
        }

        &:hover{
            .overlay{
                visibility: visible;
                
                p{
                    transform: translateY(0);
                }
            }

        }
    }
}
</style>