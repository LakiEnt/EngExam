<template>
  <div class="flex flex-center column q-mt-xl">
<!--    привязать numberQuestion.value  к q-tab-panel чтобы была красивая анимация  свайпа -->
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
const questions = [
  {
    question: "ЛУчший ЯП?",
    answers:  ['Java','JavaScript','Mocha', 'Python'],
    correctAnswer:  1
  },
  {
    question: "Не ЛУчший ЯП?",
    answers:  ['Java','JavaScript','Huskell', 'Python'],
    correctAnswer: 3
  },
  {
    question: "Возможно ЛУчший ЯП?",
    answers:  ['Java','Pascal','Mocha', 'Python'],
    correctAnswer: 2
  },
  {
    question: "Явно не лучший ЛУчший ЯП?",
    answers:  ['С++','JavaScript','Mocha', 'Python'],
    correctAnswer: 4
  }
]
export default defineComponent({
  name: 'TestPage',
  data(){
    return{
      showFinalResult: false,
      questions: questions,
      answerQuestion:'',
      numberQuestion:0,
      rightAnswers:0,
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

    }
  }
})
</script>
