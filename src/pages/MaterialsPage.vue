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
          {{progress*10}} / {{10}}
        </div>
      </div>

      <div class="q-mt-md" >
        <q-scroll-area style="height: 400px;">
          <q-list bordered separator>
          <q-item
              v-for="(material, index) in materials"
              :key="material.subject"
              @click="openDialog(index+1)"
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
                <q-icon :color="material.isFinished ? 'positive':'negative'" name="quiz" size="25px"/>
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
            <div class="text-h6"> Урок №</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            {material.text} <span> это передать через функцию</span>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum repellendus sit voluptate voluptas eveniet porro. Rerum blanditiis perferendis totam, ea at omnis vel numquam exercitationem aut, natus minima, porro labore.
          </q-card-section>

          <q-card-actions align="right">
            <q-btn flat label="Перейти к тесту (сделать через кнопку функцию котрая передавала бы данные о тесте)" @click="$router.push('/testPage')"  color="primary" v-close-popup />
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
  name: 'IndexPage',
  components: {},
  data(){
    return {
       progress:0.3,
       openDialogTest: false,
       materials: null,

    }
  },
  methods:{
    openDialog(){
      this.openDialogTest = true
    },
    // проблема: на телефоне не передается файл api
    async getMaterials() {
      const response = await fetch('src/api.json')
      const data = await response.json();
      this.materials = data.materials

    }
  },
  created() {
    this.getMaterials()
  }
})
</script>
