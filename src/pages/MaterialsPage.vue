<template>
  <q-page class="flex flex-center">
    <div class="q-px-xs q-pb-xl full-width flex column justify-center">
      <p>Cтраница со списком материалов для подготовки</p>
      <div class="bg-cyan-7 q-pa-lg rounded-borders" >
        <p>Пройденные материалы: </p>

        <q-linear-progress
            :value="progress"
            color="white"
            rounded
            size="md"
            class="q-mt-md"
        />
        <div>
          {{progress*10}} / {{10}}
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
                class="rounded-borders q-py-lg"
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
      progress:0.3,
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
  },

})
</script>

<style>


</style>
