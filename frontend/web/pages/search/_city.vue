<template>
  <v-container fluid pa-0 class="search__container">
    <v-row class="search__container__row ma-0">
      <v-col cols="12" sm="8" md="6" lg="5" xl="4" class="cards-section">
        <v-list class="cards-list pa-0">
          <v-list-item
            v-for="i in page.count"
            :key="i"
            class="cards-list__item pa-0"
          >
            <object-card></object-card>
          </v-list-item>
        </v-list>
        <v-pagination
          v-model="page.current"
          :length="3"
          color="#00ACA2"
          circle
          class="pagination pt-6"
        ></v-pagination>
      </v-col>

      <v-col
        sm="4"
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
    return {
      page: {
        count: 10,
        current: 1,
      },
    }
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
  height: calc(100vh - (90 + 133px));
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
}

.cards-section {
  padding: 0 20px 20px 20px;
}

.cards-list {
  background-color: transparent !important;

  &,
  & * {
    box-shadow: none !important;
  }
}

.cards-list__item:not(:first-of-type) {
  padding-top: 20px !important;
}

@media (max-width: 798px) {
  .search__container__row__map {
    display: none;
  }

  .cards-section {
    width: 100% !important;

    &,
    & * {
      flex: 0 0 100%;
      max-width: 100% !important;
    }
  }
}

.pagination {
  &,
  & * {
    box-shadow: none !important;
    :not(.v-pagination__item--active) {
      background-color: transparent !important;
    }

    :not(.vue-scoped-not-leaks) {
      box-shadow: none !important;
    }
  }
}
</style>
