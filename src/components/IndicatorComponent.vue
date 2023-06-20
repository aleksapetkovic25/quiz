<template>
    <div class="indicator-container">
        <img :src="'/src/assets/'+rival.img" alt="rival">
        <div v-for="(step,index) in steps" :key="step.id" class="indicator-step" 
            :class="{
            'rival': index <= rivalPosition, 
            'rival-step': rivalPosition == index, 
            'free': index > rivalPosition && index < currentPosition && currentPosition != rivalPosition, 
            'rest': index >= currentPosition && currentPosition != rivalPosition}">
                {{currentPosition == index ? "CURRENT STEP" : ""}}
        </div>
    </div>
</template>

<script>
export default {
    props: ["level", "rival"],
    data(){
        return{
            steps:[
                {
                    id: 1
                },
                {
                    id: 2
                },
                {
                    id: 3
                },
                {
                    id: 4
                },
                {
                    id: 5
                },
                {
                    id: 6
                },
                {
                    id: 7
                },
                {
                    id: 8
                }
            ],
            currentPosition: 3,
            rivalPosition: 0
        }
    },
    mounted(){
        this.setLevel();
    },
    methods:{
        setLevel(){
            if(this.level.name == 'easy'){
                this.currentPosition = 4;
            }
            if(this.level.name == 'normal'){
                this.currentPosition = 3
                return;
            }
            if(this.level.name == 'hard'){
                this.currentPosition = 2;
            }
           
        },
        checkGame(isTrue){
            if(this.currentPosition >= 7){
                return;
            }
            if(isTrue){
                this.currentPosition++;
                this.rivalPosition++;
            }
            else{
                this.rivalPosition++;
            }

            if(this.currentPosition == this.rivalPosition){
                this.$emit('checkWin', false);
            }

            if(this.currentPosition == 7){
                this.$emit('checkWin', true);
            }
        }
    }
}
</script>

<style lang="scss" scoped>
$stepHeight: 30px;
$stepWidth: 200px;


.indicator-container{
    box-sizing: content-box;
    width: $stepWidth;
    padding: 20px 30px 40px;
    background-color: #010101;
    box-shadow: 0px 0px 3px 4px rgba(33,230,255,1);
    color: #fff;
    font-weight: bold;
    text-align: center;
    line-height: $stepHeight;

    img{
        max-width: 80%;
    }

    .indicator-step{
        height: $stepHeight;
        margin: 3px auto;
    
        &.rival{
            background-color: #f9071d;
        }

        &.rival-step{
            width: 0px;
            height: 0px;
            border-style: solid;
            border-width: $stepHeight $stepWidth/2 0 $stepWidth/2;
            border-color: transparent #660b2a #660b2a #660b2a;
            transform: rotate(0deg);
        }

        &.free{
            background-color: #0caef6;
        }

        &.rest{
            background-color: #033bf2;
        }
    }


    @media screen and (max-width: 1000px){
        margin: 20px auto;
        // transform: rotate(-90deg);
        // margin: 20px auto;
        // max-width: 100%;
        
        // img{
        //     transform: rotate(90deg);
        // }
    }
}
</style>