<template>
  <q-page class="flex flex-center">
    <div class="q-px-xs q-pb-xl full-width flex column justify-center">
      <div class="row justify-between">
        <div class="col-12 bg-primary q-pa-lg rounded-borders">
          <p class="text-white">Пройденные тесты: </p>

          <q-linear-progress
              :value="progress"
              color="white"
              rounded
              size="md"
              class="q-mt-md"
          />
          <div class="text-white">
            {{progress*10}} / {{10}}
          </div>
        </div>

        <div class="col-8 bg-primary rounded-borders q-pa-lg q-mt-md flex justify-end">
          <p class="text-white">Выбрать случайный тест: </p>
          <q-btn icon="arrow_forward" color="white" outline round @click="pushToRandomTest"/>
        </div>
      </div>

      <div class="q-mt-md" >
        <q-scroll-area style="height: 400px;">
          <q-list bordered separator>
            <q-item
                v-for="n in 10"
                :key="n"
                @click="openDialog(n)"
                clickable
                v-ripple
                class="rounded-borders q-py-lg bg-white"
            >
              <q-item-section>
                <div class="q-mb-xs">
                  Название урока №{{n}}
                </div>
                <div>
                  Тема
                </div>
              </q-item-section>

              <q-item-section class="text-center">
                <div class="q-mb-xs">
                  А{{n}}
                </div>
                <div>
                  <q-icon :color="n%2 ==0 ? 'positive':'negative'" name="quiz" size="25px"/>
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
            <div class="text-h6"> Урок №{{test.question}}</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum repellendus sit voluptate voluptas eveniet porro. Rerum blanditiis perferendis totam, ea at omnis vel numquam exercitationem aut, natus minima, porro labore.
          </q-card-section>

          <q-card-actions align="right">
            <q-btn flat label="OK" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

    </Teleport>


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
      test:{
        question:'',
        time:'',
      },
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
      console.log(123)
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

    //progress test
  }

})
</script>
