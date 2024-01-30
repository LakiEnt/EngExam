<template>
  <div class="flex flex-center column q-mt-xl">
<!--    привязать numberQuestion.value  к q-tab-panel чтобы была красивая анимация  свайпа -->
    <h5> Название теста: {{ this.materials[this.numberMaterial].tests[0].nameOfTest}}</h5>

    <div v-if="!showFinalResult">
      <div>
        {{questions[numberQuestion].question}}
      </div>
      <div class="flex column">
        <q-radio
          v-model="answerQuestion"
          v-for="(answer,index) in questions[numberQuestion].answers"
          :key="answer"
          :val="index"
          :label="answer"
        />
      </div>

      <div class="q-mt-md">Вопрос {{numberQuestion + 1}} из {{questions[numberQuestion].answers.length}}</div>

      <q-btn class="q-mt-xl" label="Ответить" @click="incrementNumberTest"/>
    </div>

    <div v-if="showFinalResult">
      Ваш результат: {{rightAnswers}} / {{questions.length}}
    </div>
  </div>

</template>

<script>
import {defineComponent} from "vue";

//в целом вместе с номером тест можно передавать и вопросы
// const questions = [
//   {
//     question: "ЛУчший ЯП?",
//     answers:  ['Java','JavaScript','Mocha', 'Python'],
//     correctAnswer:  1
//   },
//   {
//     question: "Не ЛУчший ЯП?",
//     answers:  ['Java','JavaScript','Huskell', 'Python'],
//     correctAnswer: 3
//   },
//   {
//     question: "Возможно ЛУчший ЯП?",
//     answers:  ['Java','Pascal','Mocha', 'Python'],
//     correctAnswer: 2
//   },
//   {
//     question: "Явно не лучший ЛУчший ЯП?",
//     answers:  ['С++','JavaScript','Mocha', 'Python'],
//     correctAnswer: 4
//   }
// ]
export default defineComponent({
  name: 'TestPage',
  data(){
    return{
      materials: null,
      showFinalResult: false,
      questions: [],
      answerQuestion:'',
      numberQuestion:0,
      rightAnswers:0,
      numberMaterial:null,
    }
  },
  methods: {
    incrementNumberTest(){
      if(this.answerQuestion !== '') {
        if(this.answerQuestion + 1 === this.questions[this.numberQuestion].correctAnswer){
          this.rightAnswers+=1
        }
        this.numberQuestion+=1
        this.answerQuestion = ''
      }
      if(this.numberQuestion === this.questions.length){
        this.showFinalResult = true
      }

    },
    async getMaterials() {
      // const response = await fetch('src/api.json')
      // const data = await response.json();
      // this.materials = data.materials

      if(!localStorage.getItem('materials')){
        console.log('no materials in local storage')
        localStorage.setItem("materials", JSON.stringify(this.initMaterials));
        this.materials = this.initMaterials
      }
      else {
        console.log('materials in local storage')
        this.materials = JSON.parse(localStorage.getItem('materials'))
      }

      for (let material of this.materials) {
        this.progress += material.isFinished ? 1 : 0
      }
      this.progress = (this.progress / 10).toFixed(1)

    }
  },
  watch: {
    materials:{
      handler(val, newVal) {
        console.log('materials setted by watcher local storage')
        localStorage.setItem("materials", JSON.stringify(val));
      },
      deep: true
    },
  },
  created() {
    this.getMaterials()
    this.numberMaterial = this.$route.query.materialNumber
    this.questions =  this.materials[this.numberMaterial].tests[0].questions


  }
})
</script>
