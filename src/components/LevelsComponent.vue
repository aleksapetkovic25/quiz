<template>
    <div class="levels" :class="{show: showLevels && !selectedLevel, 'rotate-in': showLevels}">
        <div class="level" v-for="lvl in levels" :key="lvl.id" @click="selectLevel(lvl)">
            <img :src="'/src/assets/' + lvl.img" alt="level-icon">
            <div class="overlay">
                <p>{{lvl.name}}</p>
            </div>
        </div>
    </div>
</template>




<script>
export default {
    props: ['rival'],
    data(){
        return{
            levels: [
                {
                    name: "easy",
                    img: "easy-level.png",
                    id: 1,
                },
                {
                    name: "normal",
                    img: "medium-level.png",
                    id: 2,
                },
                {
                    name: "hard",
                    img: "hard-level.png",
                    id: 3,
                }
            ],
            selectedLevel: null,
            showLevels: false

        }
    },
    methods: {
        selectLevel(level){
            this.selectedLevel = level;
            this.$emit('selectedLevel', level);
        }
    },
    watch:{
        rival(){
            if(this.rival){
                setTimeout(() => {
                    this.showLevels = true
                }, 290);
            }
        }
    }
}
</script>



<style lang="scss" scoped>
$borderRadius: 20px;
.levels{
    display: none;
    justify-content: space-between;

    &.show{
        display: flex;
    }

    .level{
        position: relative;
        width: 30%;
        border-radius: $borderRadius;
        box-shadow: 0px 0px 8px 1px rgba(71,71,71,0.93);
        background-color: rgb(39, 39, 39);
        text-align: center;
        padding: 50px 0;

        img{
            max-width: 60%;
        }

        .overlay{
            position: absolute;
            border-radius: $borderRadius;
            display: flex;
            visibility: hidden;
            justify-content: center;
            align-items: center;

            p{
                transform: translateY(100px);
                transition: transform 1s ease;
                color: #fff;
                text-transform: uppercase;
                font-weight: 700;
            }

        }

        &:hover{
            .overlay{
                visibility: visible;
                
                p{
                    transform: translateY(0);
                    letter-spacing: 15px;
                    font-size: 25px;
                }
            }

        }
    }
}
</style>