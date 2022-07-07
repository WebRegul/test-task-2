<template>
  <v-app-bar
    light
    app
    elevation="0"
    height="90px"
  >
    <v-btn icon color="red" class="ml-5">
      <v-icon x-large>{{ logo }}</v-icon>
    </v-btn>
    <v-toolbar-title v-text="title" />
    <v-spacer />
    <small-search-form
      v-if="search"
      class="align-content-center"
      short
    ></small-search-form>
    <v-spacer />
    <v-btn
      outlined
      width="138px"
      color="#00ACA2"
      class="mr-md-2 text-capitalize font-weight-regular py-6 px-8 rounded-lg bg-white body-1"
      >Вход</v-btn
    >
    <v-btn
      rounded
      outlined
      raised
      width="138px"
      color="#00ACA2"
      class="text-capitalize font-weight-regular py-6 px-8 rounded-lg bg-white body-1"
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

<style scoped></style>
