<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          EngExam
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Меню
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <div class="full-width flex justify-around q-py-lg bg-grey-5 fixed-bottom" style="border-radius:20px 20px 0 0">
      <q-btn flat rounded v-for="link in essentialLinks" :key="link.name"  @click="$router.push(link.link)">
        <q-icon :color="link.link === $route.path ? 'cyan-7' : '' " :name="link.icon" size="35px"/>
      </q-btn>
    </div>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Тесты',
    caption: 'Выбрать тест',
    icon: 'book',
    link: '/'
  },
  {
    title: 'Материалы',
    caption: 'Уроки для изучения',
    icon: 'description',
    link: '/materials'
  },
  {
    title: 'Любимое',
    caption: 'Ваши сохраненные тесты или уроки',
    icon: 'favorite_border',
    link: '/favourites'
  },
  {
    title: 'Настройки',
    caption: 'Настройте шрифт или цвет приложения',
    icon: 'settings',
    link: '/settings'
  },

]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style lang="scss" scoped>

</style>
