<template>
  <div id="app">
    <Header
            :score="score"
    />
    <QuestionBox v-if="questions.length"
         :currentQuestion="questions[questIndex]"
         :next="next"
         :questIndex="questIndex"
                 :EvaluateAnsColor="EvaluateAnsColor"
                 :ansClicked="ansClicked"
                 :ansClickFun="ansClickFun"
                 :response="response"
    />
  </div>
</template>

<script>
    import Header from './components/Header.vue'
    import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    QuestionBox,
    Header
  },
    data(){
        return {
            score:0,
            questIndex: 0,
            questions: [],
            ansClicked: false,
            response : 'choose one answer from the above'
        }

    },
    methods:{
        next(){
            this.questIndex++
            this.ansClicked = false
        },
        EvaluateAnsColor(answer){
            if(this.ansClicked){
                if(answer === this.questions[this.questIndex].correctAnswer)
                {
                    return "success"
                }
                else
                    return "danger"
            }
            else{
                return ''
            }
        },
        ansClickFun(answer){
            this.ansClicked = true
            if(this.EvaluateAnsColor(answer)==='success'){
                this.score++
                this.response = 'Great Job ! '
            }
            else{
                this.response = 'Oops, wrong answer. Good luck next time!'
            }

        }
    },
    mounted: function () {
        fetch('https://trivia.willfry.co.uk/api/questions?categories=movies&limit=11', {
            method: 'get',
        })
            .then(response => response.json())
            .then(jsonData => {
                this.questions = jsonData
            })

    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
