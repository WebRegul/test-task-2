<template>
  <v-footer class="footer" padless fixed light>
    <v-row justify="center" no-gutters>
      <v-col class="pt-5 text-center" cols="12">
        <v-btn v-for="link in links" :key="link" text rounded>
          {{ link }}
        </v-btn>
      </v-col>

      <v-col class="pt-3 text-center" cols="12">
        <div class="hor-line"></div>
      </v-col>

      <v-col class="text-center">
        <v-btn v-for="icon in icons" :key="icon" class="mx-4" icon>
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
      </v-col>

      <v-col class="text-center" cols="12">
        {{ new Date().getFullYear() }} — <strong class="text-subtitle-1">ООО "Понаехали"</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
  name: 'BaseFooter',
  data: () => ({
    icons: ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram'],
    links: [
      // 'Главная',
      // 'Поиск',
      // 'Войти',
      // 'Куда-то пойти',
      // 'Регистрация',
      // 'Контакты',
      'О проекте',
      'Руководство',
      'Правила',
      'Помощь',
    ],
  }),
}
</script>

<style lang="scss" scoped>
.footer {
  background-color: #ebebec;

  &,
  & * {
    color: #5f5f61 !important;
    text-transform: none;
  }

  .hor-line {
    width: 62.46vw;
    height: 1px;
    background-color: #5F5F61;
    margin: 0 auto;
  }
}
</style>
