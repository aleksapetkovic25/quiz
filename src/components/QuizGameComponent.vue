<template>
    <div class="game-container">
        <div class="question-container">
            {{question.question}}
        </div>
        <div class="answers-contaier">
            <div class="answer" v-for="(answer, index) in question.answers" :key="index" @click="checkAnswer($event, answer)">
                {{ abcd(index) + answer.answer}}
            </div>
            <!-- <div class="answer">
                B: {{answer.answer}}
            </div>
            <div class="answer">
                C: {{answer.answer}}
            </div>
            <div class="answer">
                D: {{answer.answer}}
            </div> -->
        </div>
    </div>
</template>

<script>
import questions from '../../questions.json'

export default {
    data(){
        return{
            questions: [],
            question: null,
        }
    },
    created(){
        this.questions = JSON.parse(JSON.stringify(questions));
        // this.questions = Object.values(this.questions)
        this.getQuestion();
    },
    methods:{
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
            if(answer.isTrue){
                e.target.classList.add('asd')
                console.log(e.target)
                console.log("tacno")
            }else{
                console.log("netacno")
            }
            this.getQuestion()
        },
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
        }
    }
}
</script>

<style lang="scss" scoped>

.game-container{

    width: 800px;
    margin: 0 auto;
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

        }
    }
}
</style>