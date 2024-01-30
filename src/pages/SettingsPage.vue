<template>
  <q-page class="flex column q-pt-xl q-px-xs">
    <p class="q-pl-md q-mb-xl"> Настройки </p>
    <div>
      <q-list>
        <q-item class="flex column justify-start">
          <div class="q-mb-lg">
            Цвет главной темы:
          </div>
          <div class="flex">
            <q-color
              v-model="hex"
              v-for="color in palette"
              :key="color"
              :palette="[color]"
              no-footer
              no-header
              no-header-tabs
              default-view="palette"
              class="q-ma-xs rounded-borders"
              :style="`background-color:${color}; min-width:50px; min-height:50px`"
              @click="changeColorTheme(color)"
            />
          </div>
        </q-item>

        <q-separator spaced/>

        <q-item class="flex column justify-start">
          <div class="q-mb-lg">
            Размер шрифта:
          </div>
          <div class="flex">
            <q-chip
              size="18px"
              v-for="(fontElem, index) in fontSizes"
              :key="fontElem.name"
              v-model="font"
              :selected="fontSizes[index].size === font"
              color="primary"
              text-color="white"
              @click="changeFontSize(fontElem.size)"
            >
              {{fontElem.name}}
            </q-chip>
          </div>
        </q-item>

        <q-separator class="q-my-md"/>

        <q-item class="flex column justify-start">
          <div class="q-mb-lg">
           Выбор языка:
          </div>
          <div class="flex">
            <q-chip
              size="18px"
              selected
              color="primary"
              text-color="white"
              label="Русский"
            />
          </div>
        </q-item>
      </q-list>
    </div>


  </q-page>
</template>

<script>
export default {
  name: "SettingsPage",
  data(){
    return{
      hex: '#FF00FF',
      font:'16px',
      palette: ['#009999', '#D9B801', '#E8045A', '#B2028A'],
      fontSizes: [
        {
          name:'xs',
          size: '12px'
        },
        {
          name:'md',
          size: '16px'
        },
        {
          name:'lg',
          size: '20px'
        },
        {
          name:'xl',
          size: '24px'
        },
      ]


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
  }
}
</script>
