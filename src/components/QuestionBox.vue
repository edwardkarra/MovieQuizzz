<template>
    <div class="col-12">
        <div class="col-8 offset-2">
            <b-card  :title="currentQuestion.question" header-tag="header" footer-tag="footer">
                <template #header>
                        <p class="mb-0">Question Number : {{questIndex+1}}</p>
                </template>
                <b-card-text v-for="(answer,index) in Answers" :key="index">
                    <b-button href="#"  :variant="EvaluateAnsColor(answer)" @click="ansClickFun(answer)" :disabled="ansClicked">
                        {{answer}}
                    </b-button>
                </b-card-text>
                <template #footer>
                    <em>{{response}}</em>
                </template>
            </b-card>
        </div>
        <br/>
        <b-button @click="next" :disabled="questIndex>=9" variant="primary" class="col-6 ">Next</b-button>

    </div>
</template>
<script>
    export default {
        props:{
            next : Function,
            questIndex : Number,
            currentQuestion : Object,
            EvaluateAnsColor : Function,
            ansClicked : Boolean,
            ansClickFun : Function,
            response : String
        },
        data(){
            return{
                num : 0
            }
        },
        computed:{
            Answers(){
                let choices = []
                let incorrectAnsNumber = this.currentQuestion['incorrectAnswers'].length
                for (let i=0;i<(Math.min(3,incorrectAnsNumber));){
                    let rand = Math.floor(Math.random() * incorrectAnsNumber);
                    let choice = this.currentQuestion['incorrectAnswers'][rand];

                    if(!choices.includes(choice)){
                        choices.push(choice)
                        i++
                    }
                }
                choices.push(this.currentQuestion.correctAnswer)
                choices.sort(() => Math.random() - 0.5)
                for(let i=0;i<choices.length;i++)
                    console.log(`this is ${i}: ${choices[i]}`)
                return choices
            },

        },
    }
</script>
