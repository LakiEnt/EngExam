<template>
  <q-page class="flex flex-center">
    <div class="q-px-md q-pb-xl full-width flex column justify-center">
      <div class="row justify-between">
        <div class="col-12 bg-primary q-pa-lg rounded-borders">
          <p class="text-white">{{localization.testsPage.title}}: </p>
          <q-linear-progress
              :value="progress/10"
              color="white"
              rounded
              size="md"
              class="q-mt-md"
          />
          <div class="text-white">
            {{progress*10}} / {{tests.length}}
          </div>
        </div>

        <div class="col-8 bg-primary rounded-borders q-pa-lg q-mt-md flex  justify-start">
          <p class="text-white">{{ localization.testsPage.toRandomTestBtnText }}: </p>
          <q-btn icon="arrow_forward" color="white" outline round @click="pushToRandomTest"/>
        </div>
      </div>

      <div class="q-mt-md" >
        <q-scroll-area style="height: 400px;">
          <q-list separator>
            <q-item
               v-for="(test, index) in tests"
                :key="test.subject"
                clickable
                v-ripple
                class="rounded-borders q-py-xs q-mb-md bg-white"
               @click="$router.push(`/testPage?materialNumber=${index}`)"
            >
              <q-item-section>
                <div class="row items-center">
                  <div class="col-10">
                    <div class="q-mb-xs">
                      {{ localization.testsPage.test.testName }}: {{ test.nameOfTest.length > 19 ? test.nameOfTest.slice(0,19) + '...' : test.nameOfTest  }}
                    </div>
                     <div>
                       {{ localization.testsPage.test.subject }}: {{ test.subjectOfTest }}
                    </div>
                  </div>

                  <div class="col-2">
                    <div class="q-mb-xs">
                      {{ test.level }}
                    </div>
                    <div>
                      <q-icon :color="test.isFinished ? 'positive':'negative'" name="quiz" size="25px"/>
                    </div>
                  </div>
                </div>
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>
      </div>
    </div>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MaterialsPage',
  data(){
    return {
      materials: null,
      progress: 0,
      openDialogTest: false,
      tests:[],
      localization: null,
    }
  },
  methods:{
    openDialog(n){
      this.openDialogTest = true
      this.test.question = n
    },
    pushToRandomTest(){
      const max = this.materials.length
      const min = 0
      const minCeiled = Math.ceil(min);
      const maxFloored = Math.floor(max);

      const randomTestIndex = Math.floor(Math.random() * (maxFloored - minCeiled) + minCeiled);
      this.$router.push(`/testPage?materialNumber=${randomTestIndex}`)
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
    },
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

    //need all tests
    for (let index of this.materials) {
      console.log(index.tests, 'test')
      const test = {
        'nameOfTest': index.tests[0].nameOfTest,
        'isFinished': index.tests[0].isFinished,
        'subjectOfTest': index.subject,
        'level': index.level
      }
      if(index.tests[0].isFinished) {
        this.progress = this.progress + 1
        console.log(this.progress, 'indexxxxx')
      }
      this.tests.push(test)
    }
    this.progress = (this.progress / 10).toFixed(1)

    //progress test

    this.localization = JSON.parse(localStorage.getItem("localization"))
  }

})
</script>
