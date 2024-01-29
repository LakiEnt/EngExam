<template>
    <div class="q-mt-xl q-px-xs">


        <q-tabs
            v-model="tab"
            dense
            align="left"
            class="bg-cyan-7 text-white shadow-2 rounded-borders"
            style="max-width: fit-content"
            :breakpoint="0"
        >
          <q-tab class="q-px-xl" name="mails">Тесты</q-tab>
          <q-tab class="q-px-xl" name="alarms"  >Уроки</q-tab>
        </q-tabs>

        <q-tab-panels  class="rounded-borders" swipeable v-model="tab" animated>
          <q-tab-panel  name="mails">
            <div class="text-h6">Тесты</div>
            <div class="q-mt-md" >
              <q-scroll-area style="height: 500px;">
                <q-list bordered separator>
                  <q-item
                      v-for="n in 10"
                      :key="n"
                      clickable
                      v-ripple
                      class="rounded-borders q-py-lg"
                  >
                    <q-item-section>
                      <div class="q-mb-xs">
                        Название теста №{{n}}
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

          </q-tab-panel>

          <q-tab-panel name="alarms">
            <div class="text-h6">Уроки</div>
            <div class="q-mt-md" >
              <q-scroll-area style="height: 500px">
                <q-list bordered separator>
                  <q-item
                      v-for="n in 10"
                      :key="n"
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
          </q-tab-panel>
        </q-tab-panels>
    </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'FavouritesPage',
  data(){
    return{
      tab: 'mails',
    }
  }
})
</script>
