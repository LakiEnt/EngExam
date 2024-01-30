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

    <q-page-container class="bg-grey-3">
      <router-view />
    </q-page-container>

    <div class="full-width flex justify-around q-py-lg fixed-bottom bg-white" style="border-radius:20px 20px 0 0">
      <q-btn flat rounded v-for="link in essentialLinks" :key="link.name"  @click="$router.push(link.link)">
        <q-icon :color="link.link === $route.path ? 'primary' : '' " :name="link.icon" size="35px"/>
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
  data() {
    return {
     hex:'',
     font:''
    }
  },

  methods: {
    changeColorTheme(color){
      document.documentElement.style.setProperty('--q-primary', color);
      localStorage.setItem("color", color);
    },
    changeFontSize(size){
      this.font = size
      document.body.style.setProperty('font-size', size);
      localStorage.setItem("font-size", size);
    }
  },
  created() {
    if(localStorage.getItem("color")) {
      this.hex = localStorage.getItem("color")
      this.changeColorTheme(localStorage.getItem("color"))
    }
    if(localStorage.getItem("font-size")) {
      this.hex = localStorage.getItem("font-size")
      this.changeFontSize(localStorage.getItem("font-size"))
    }
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
