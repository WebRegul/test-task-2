<template>
  <v-app-bar light app align-start elevation="0" class="app-bar pt-4">
    <v-icon icon color="#00ACA2" x-large>{{ logo }}</v-icon>
    <v-toolbar-title class="logo__title" v-text="title" />
    <v-spacer />
    <small-search-form v-if="search" short></small-search-form>
    <v-spacer />
    <v-btn
      outlined
      width="138px"
      color="#00ACA2"
      class="btn__login ml-5 mr-2 text-capitalize font-weight-regular py-6 px-8 rounded-lg bg-white body-1"
      >Вход</v-btn
    >
    <v-btn
      rounded
      outlined
      raised
      width="138px"
      color="#00ACA2"
      class="btn__register text-capitalize font-weight-regular py-6 px-8 rounded-lg bg-white body-1"
      >Регистрация</v-btn
    >
  </v-app-bar>
</template>

<script>
import { mdiBiohazard } from '@mdi/js'
import { mapGetters } from 'vuex'
import SmallSearchForm from '../../components/forms/search/SmallSearchForm'
// import Registration from '../../components/cabinet/Registration'
// import SmsConfirm from '../../components/cabinet/SmsConfirm'
// import Login from '../../components/cabinet/Login'

export default {
  name: 'BaseHeader',
  components: { SmallSearchForm },
  props: {
    search: {
      type: Boolean,
      default: false,
    },
  },

  data: () => ({
    logo: mdiBiohazard,
    title: 'Понаехали!',
  }),

  computed: {
    ...mapGetters({}),
  },

  methods: {
    toggleVisible(type, value) {},
  },
}
</script>

<style lang="scss" scoped>
.app-bar {
  &,
  & > * {
    height: 90px !important;
  }
}

@media (max-width: 1018px) {
  .logo__title {
    display: none;
  }

  @media (max-width: 794px) {
    .btn__login,
    .btn__register {
      display: none;
    }

    .app-bar {
      &,
      & > * {
        height: 60px !important;
        padding: 0 calc(4.2vw - 15px);
      }
    }
  }
}
</style>
