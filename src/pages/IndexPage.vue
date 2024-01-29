<template>
  <q-page class="flex flex-center">
    <div>
      <h3> Страница со списком тестов </h3>
      <div class="q-pa-md" style="max-width: 350px">
        <q-list bordered separator>
          <q-item v-for="n in 10" :key="n" clickable v-ripple>
            <q-item-section>Вопрос номер: {{n}}</q-item-section>
            <q-item-section>Тема вопроса: {{n}}</q-item-section>
            <q-item-section>Уровень подготовки: А{{n}}</q-item-section>
            <q-item-section>Выполнен ли: А{{n}}</q-item-section>
          </q-item>
        </q-list>
      </div>
    </div>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage'
})
</script>
