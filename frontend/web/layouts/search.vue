<template>
  <v-app light>
    <base-header search />
    <full-search-form></full-search-form>
    <v-main app class="search-page__main pa0">
      <Nuxt />
    </v-main>
  <base-footer />
  </v-app>
</template>

<script>
import FullSearchForm from '../components/forms/search/FullSearchForm'
import BaseFooter from './includes/BaseFooter.vue'
import BaseHeader from './includes/BaseHeader'
export default {
  name: 'SearchLayout',
  components: { FullSearchForm, BaseHeader, BaseFooter, },
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
    }
  },
  computed: {
    isFullPage() {
      return (
        this.$route.matched.map((r) => {
          return r.components.default.options.isFullPage
        })[0] || false
      )
    },
  },
}
</script>
<style lang="scss" scoped>
.search-page__main {
  padding-top: 180px !important;

  @media (max-width: 798px) {
    padding-top:  120px !important;
  }
}
</style>
