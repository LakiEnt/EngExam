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
    question: "Choose the correct verb form in the present simple tense: \n He usually _______ breakfast at 7 am.",
    answers:  ['eat','eating','ate', 'eats'],
    correctAnswer:  1
  },
  {
    question: "Choose the correct verb form in the present continuous tense:\nThey _______ a movie right now.",
    answers:  ['watch','watching','watched', 'watches'],
    correctAnswer: 2
  },
  {
    question: "Choose the correct verb form in the past simple tense:\nWe _______ to the beach last weekend.",
    answers:  ['go','going','went', 'goes'],
    correctAnswer: 3
  },
  {
    question: "Choose the correct verb form in the future continuous tense:\nThey _______ a party on Saturday evening.",
    answers:  ['plan','planning','planned', 'will be planning'],
    correctAnswer: 4
  },
  {
    question: "Choose the correct verb form in the present perfect tense:\nShe _______ the book already.",
    answers:  ['read','reading','reads', 'has read'],
    correctAnswer: 4
  }
  ,
  {
    question: "Choose the correct verb form in the future perfect tense:\nBy next year, I _______ the language.",
    answers:  ['learn','learning','will learn', 'would learn'],
    correctAnswer: 3
  }
  ,
  {
    question: "Choose the correct verb form in the present perfect continuous tense:\nWe _______ for six hours.",
    answers:  ['study','studying','studied', 'have been studying'],
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
