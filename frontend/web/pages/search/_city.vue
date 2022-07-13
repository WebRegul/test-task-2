<template>
  <v-container fluid pa-0 class="search__container">
    <v-row class="search__container__row ma-0">
      <v-col cols="12" sm="12" md="6" lg="5" xl="4" class="cards-section">
        <v-list class="cards-list pa-0">
          <v-list-item v-for="i in 10" :key="i" class="cards-list__item pa-0">
            <object-card></object-card>
          </v-list-item>
        </v-list>
      </v-col>

      <v-col
        md="6"
        lg="7"
        xl="8"
        class="flex-column align-end pa-0 search__container__row__map"
      >
        <search-map @update:bounds="updateMapBoundsHandler"></search-map>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapActions } from 'vuex'
import ObjectCard from '../../components/cards/ObjectCard'
import SearchMap from '../../components/maps/SearchMap'

export default {
  name: 'SearchPage',
  components: { SearchMap, ObjectCard },
  layout: 'search',
  data() {
    return {}
  },
  computed: {},
  mounted() {
    this.list()
  },
  methods: {
    ...mapActions({
      list: 'web/search/getList',
      map: 'web/search/getPoints',
    }),
    updateMapBoundsHandler(bounds) {
      console.log('updateMapBoundsHandler', bounds)
      this.map(bounds)
    },
  },
}
</script>

<style lang="scss" scoped>
.search__container {
  height: calc(100vh - 90px);
  background-color: transparent;
  overflow-y: auto;
  overflow-x: hidden;
}

.search__container__row {
  min-height: 100%;
}

.search__container__row__map {
  position: fixed;
  right: 0px;
  height: 100%;

  @media (max-width: 798px) {
    display: none;
  }
}

.cards-section {
  padding: 0 20px 20px 20px;
}

.cards-list {
  background-color: transparent;
}

.cards-list__item:not(:first-of-type) {
  padding-top: 20px !important;
}
</style>
