<template>
    <div style="width: 100%;">
        <div v-if="message" class="end-game">
            <h2>{{message}}</h2>
            <button @click="playAgain">Play Again</button>
        </div>
        <div class="quiz">
            <div class="game-container">
                <div class="question-container">
                    {{question.question}}
                </div>
                <div class="answers-contaier">
                    <div class="answer" v-for="(answer, index) in question.answers" :key="index" @click="checkAnswer($event, answer)">
                        {{ abcd(index) + answer.answer}}
                    </div>
                </div>
            </div>
            <IndicatorComponent ref="indicator" @checkWin="checkWin" :level="level" :rival="rival"></IndicatorComponent>
        </div>
    </div>
</template>

<script>
import questions from '../../questions.json'
import IndicatorComponent from './IndicatorComponent.vue'

export default {
    components: {IndicatorComponent},
    props: ['level', 'rival'],
    data(){
        return{
            questions: [],
            question: null,
            click: false,
            message: null
        }
    },
    created(){
        this.questions = JSON.parse(JSON.stringify(questions));
        // this.questions = Object.values(this.questions)
        this.getQuestion();
    },
    methods:{
        abcd(index){
            switch(index){
                case 0:
                    return "A: ";
                case 1:
                    return "B: ";
                case 2:
                    return "C: ";
                case 3:
                    return "D: ";
                default:
                    return "E: ";
            }
        },
        getQuestion(){
            if(this.questions.length == 0){
                console.log("Nema vise pitanja");
                return;
            }
            // Uzimamo pitanje koje se postavlja igracu
            let random = Math.floor(Math.random() * this.questions.length);
            this.question = this.questions[random]
            this.randomOrderAnswers(this.question.answers);
            // Uklanjamo uzeto pitanje iz niza da se ne bi opet ponovilo
            this.questions.splice(random, 1);
        },
        randomOrderAnswers(arr){
            for (let i = 0; i < arr.length; i++) {
                // Generišite nasumičan indeks od 0 do i
                const j = Math.floor(Math.random() * arr.length);
                
                // Zamena elemenata na pozicijama i i j
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
        },
        checkAnswer(e, answer){
            if(this.click){
                return;
            }
            this.click = true;

            if(answer.isTrue){
                e.target.classList.add('true');
                this.$refs.indicator.checkGame(true)
            }else{
                e.target.classList.add('false');
                this.$refs.indicator.checkGame(false)
            }


            setTimeout(() => {
                e.target.classList.remove('true', 'false');
                this.getQuestion()
                this.click = false;
            }, 1000);
        },
        checkWin(data){
            this.message = data ? "Congratulations. You won!" : "We are sorry, you lost."
        },
        playAgain(){
            location.reload()
        }
        
    }
}
</script>

<style lang="scss" scoped>

.end-game{
    position: fixed;
    top: 0;
    left: 0;
    z-index: 22222;
    width: 100%;
    height: 100vh;
    background: #000000e7;
    text-align: center;
    color: #fff;

    h2{
        margin-top: 15%;
        font-size: 30px;
    }

    button{
        margin-top: 20px;
        color: #fff;
        font-size: 16px;
        border: none;
        background-color: rgb(17, 113, 238);
        padding: 13px 30px;
        cursor: pointer;
    }
}

.quiz{
    display: flex;
    justify-content: space-around;
    align-items: center;
 
    .game-container{
    
        width: 1000px;
        color: #fff;
    
        .question-container{
            border: 3px solid #fff;
            border-radius: 30px;
            padding: 20px;
            margin-bottom: 50px;
        }
    
        .answers-contaier{
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
    
            .answer{
                border: 3px solid #fff;
                border-radius: 20px;
                width: 49.0%;
                margin: 10px 0;
                padding: 10px;
                cursor: pointer;
    
                &.true{
                    background: rgb(16, 158, 16);
                }
    
                &.false{
                    background: red;
                }
            }
        }
    }
}
</style>