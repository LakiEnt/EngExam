<template>
  <q-page class="flex flex-center">
    <div class="q-px-xs q-pb-xl full-width flex column justify-center">
      <div class="bg-primary q-pa-lg rounded-borders">
        <p class="text-white">Пройденные материалы: </p>

        <q-linear-progress
            :value="progress"
            color="white"
            rounded
            size="md"
            class="q-mt-md"
        />
        <div class="text-white">
          {{progress*10}} / {{materials.length}}
        </div>
      </div>

      <div class="q-mt-md" >
        <q-scroll-area style="height: 400px;">
          <q-list bordered separator>
          <q-item
              v-for="(material, index) in materials"
              :key="material.subject"
              @click="openDialog(index)"
              clickable
              v-ripple
              class="rounded-borders q-py-lg bg-white"
          >
            <q-item-section>
              <div class="q-mb-xs">

                Название урока №{{index+1}}
              </div>
              <div>
                Тема: {{ material.subject }}
              </div>
            </q-item-section>

            <q-item-section class="text-center">
              <div class="q-mb-xs">
                {{ material.level }}
              </div>
              <div>
                <q-icon @click="material.isFinished = !material.isFinished " :color="material.isFinished ? 'positive':'negative'" name="quiz" size="25px"/>
              </div>
            </q-item-section>
          </q-item>
        </q-list>
        </q-scroll-area>
      </div>
    </div>

    <Teleport to="body">
      <q-dialog v-model="openDialogTest">
        <q-card>
          <q-card-section>
            <div class="text-h6"> Урок №{{testIndex}}</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            {material.text} <span> это передать через функцию</span>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum repellendus sit voluptate voluptas eveniet porro. Rerum blanditiis perferendis totam, ea at omnis vel numquam exercitationem aut, natus minima, porro labore.
          </q-card-section>

          <q-card-actions align="right">
            <q-btn flat label="Перейти к тесту (сделать через кнопку функцию котрая передавала бы данные о тесте)" @click="$router.push(`/testPage?materialNumber=${testIndex}`)"  color="primary" v-close-popup />
            <q-btn flat label="OK" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

    </Teleport>


  </q-page>
</template>

<script>
const materials =  [
    {
      "subject": "grammar",
      "level": "A1",
      "isFinished": true,
      "favourite": false,
      "text": "some random text maybe Lorem Ipulum",
      "tests": [
        {
          "isFinished": false,
          "nameOfTest": "times test",
          "questions":[
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
        }
      ]
    },
    // {
    //   "subject": "times",
    //   "level": "B1",
    //   "isFinished": false,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "times test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "verbs",
    //   "level": "C2",
    //   "isFinished": true,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "verbs test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "times",
    //   "level": "B2",
    //   "isFinished": true,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "grammar test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "grammar",
    //   "level": "A1",
    //   "isFinished": false,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "grammar test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "grammar",
    //   "level": "A1",
    //   "isFinished": true,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "grammar test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "grammar",
    //   "level": "A1",
    //   "isFinished": true,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "grammar test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // },
    // {
    //   "subject": "grammar",
    //   "level": "A1",
    //   "isFinished": true,
    //   "favourite": false,
    //   "text": "some random text maybe Lorem Ipulum",
    //   "test": [
    //     {
    //       "nameOfTest": "grammar test",
    //       "questions": [
    //         {
    //           "questionText": "Не ЛУчший ЯП?",
    //           "answers":  ["Java","JavaScript","Huskell", "Python"],
    //           "correctAnswer": 3
    //         }
    //       ]
    //     }
    //   ]
    // }
  ]


import { defineComponent } from 'vue'
export default defineComponent({
  name: 'IndexPage',
  components: {},
  data(){
    return {
       progress:0.3,
       openDialogTest: false,
       materials: null,
       initMaterials: materials,
       testIndex: 0,
    }
  },
  methods:{
    openDialog(n){
      this.openDialogTest = true
      this.testIndex = n
    },
    // проблема: на телефоне не передается файл api
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
  }
})
</script>
