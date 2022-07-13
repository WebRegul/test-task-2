<template>
  <v-app-bar fixed app elevation="0" class="app-bar d-flex pt-2">
    <v-select
      v-model="filters.houseType"
      label="Тип жилья"
      :items="houseTypes"
      item-text="title"
      item-value="id"
      multiple
      filled
      solo
      flat
      chips
      deletable-chips
      hide-details
      class="full_search__panel__select--house-types font-weight-regular rounded-lg bg-white mr-4"
    >
      <!-- <template v-for="item in houseTypes">
        <option :key="item.id" value="item.id">
          {{item.title}}
        </option>
      </template> -->
      <!-- <template v-slot:selection="{ item, index }">
        <v-chip v-if="index < 2">
          <span>{{ item.title }}</span>
        </v-chip>
        <span v-if="index >= 2" class="grey&#45;&#45;text text-caption">
          (и еще {{ filters.houseType.length - 2 }})
        </span>
      </template> -->
    </v-select>

    <span class="vertical-separator">
      <VerticalSeparator />
    </span>

    <v-chip-group
      v-model="filters.options"
      multiple
      class="filter-group py-0 ml-4 mr-2"
    >
      <v-chip
        v-for="item in optionsList"
        v-show="item.primary"
        :key="item.id"
        :value="item.id"
        style="border: 1px solid #d7d7d8; height: 58px"
        class="filter-group__element py-0 my-0 text-capitalize font-weight-regular py-6 px-8 rounded-lg body-1"
        :class="{
          'bg-white': !filters.options.includes(item.id),
          'filter-selected': filters.options.includes(item.id),
        }"
        >{{ item.title }}</v-chip
      >
    </v-chip-group>

    <span class="vertical-separator">
      <VerticalSeparator />
    </span>

    <v-dialog
      v-model="advancedFiltersShow"
      persistent
      scrollable
      max-width="700px"
    >
      <template #activator="{ on, attrs }">
        <v-badge
          :content="filterCount"
          :value="filterCount"
          color="#33BDB5"
          overlap
        >
          <v-btn
            filled
            solo
            text
            elevation="0"
            chips
            deletable-chips
            hide-details
            style="
              border: 1px solid #d7d7d8;
              height: 58px;
              text-transform: none;
              font-size: 16px;
              border-radius: 12px;
            "
            class="full_search__panel__select--house-types all-filters__btn font-weight-regular rounded-lg bg-white ml-4"
            :class="{
              'bg-white': !filters.options.length,
              'filter-selected': filters.options.length,
            }"
            v-bind="attrs"
            v-on="on"
          >
            Все фильтры
            <v-icon color="#37373A">mdi-dots-vertical</v-icon>
            <!-- <v-icon>mdi-format-list-bulleted-square</v-icon> -->
          </v-btn>
        </v-badge>
      </template>
      <v-card>
        <v-toolbar dark color="secondary">
          <v-card-title>
            <span class="text-h5">Фильтры</span>
          </v-card-title>
        </v-toolbar>

        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-card-title>Тип жилья</v-card-title>
                <v-chip-group
                  v-model="filters.houseType"
                  column
                  multiple
                  class="ml-2 mb-4"
                >
                  <v-chip
                    v-for="item in houseTypes"
                    :key="item.id"
                    color="primary"
                    class="advanced_filters__v-chip advanced_filters__house_type"
                    outlined
                    label
                    x-large
                    filter
                    :value="item.id"
                  >
                    {{ item.title }}
                    <v-icon right>{{ item.icon }}</v-icon>
                  </v-chip>
                </v-chip-group>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-row>
              <v-col cols="12">
                <v-card-title>Желаемая стоимость за сутки</v-card-title>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-row>
              <v-card-title>Удобства и опции</v-card-title>
              <v-col cols="12" md="12" class="pb-12">
                <v-row>
                  <v-flex
                    v-for="item in optionsList"
                    :key="item.id"
                    md6
                    shrink
                    grow
                  >
                    <v-checkbox
                      v-model="filters.options"
                      :value="item.id"
                      :label="item.title"
                      color="secondary"
                      hide-details
                    ></v-checkbox>
                  </v-flex>
                </v-row>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-row>
              <v-card-title>Правила проживания</v-card-title>
              <v-col cols="12" md="12">
                <v-row>
                  <v-flex v-for="item in rules" :key="item.id" md6 shrink grow>
                    <v-checkbox
                      v-model="filters.rules"
                      :value="item.id"
                      :label="item.title"
                      color="secondary"
                      hide-details
                    ></v-checkbox>
                  </v-flex>
                </v-row>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions class="elevation-1">
          <v-btn
            color="secondary darken-1"
            text
            @click="advancedFiltersShow = false"
          >
            Сбросить фильтры
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            color="primary darken-1"
            text
            outlined
            @click="advancedFiltersShow = false"
          >
            Смотреть предложения
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app-bar>
</template>

<script>
import VerticalSeparator from '../../base/VerticalSeparator.vue'

export default {
  name: 'FullSearchForm',
  components: {
    VerticalSeparator,
  },
  data() {
    return {
      houseTypes: [
        { id: '1', name: 'flat', title: 'Квартира', icon: 'mdi-pentagram' },
        {
          id: '2',
          name: 'room',
          title: 'Комната',
          icon: 'mdi-tag-arrow-right-outline',
        },
        { id: '33', name: 'dom', title: 'Дом', icon: 'mdi-home-outline' },
        { id: '44', name: 'hostel', title: 'Хостел', icon: 'mdi-sofa-outline' },
      ],
      optionsList: [
        { id: '1', name: 'wifi', title: 'Wi-Fi', order: -1, primary: true },
        { id: '9', name: 'kam', title: 'Камин', order: 0, primary: true },
        {
          id: '2',
          name: 'cond',
          title: 'Кондиционер',
          order: 1,
          primary: true,
        },
        {
          id: '3',
          name: 'stir',
          title: 'Стиральная машина',
          order: 2,
          primary: false,
        },
        { id: '4', name: 'utug', title: 'Утюг', order: 3, primary: true },
        { id: '5', name: 'fen', title: 'Фен', order: 4, primary: true },
        { id: '6', name: 'kuh', title: 'Кухня', order: 5, primary: true },
        { id: '7', name: 'tele', title: 'Телевизор', order: 6, primary: false },
        { id: '8', name: 'dza', title: 'Джакузи', order: 7, primary: false },
      ],
      rules: [
        {
          id: '1',
          name: 'smoking',
          title: 'Можно курить',
          order: 0,
          primary: true,
        },
        {
          id: '2',
          name: 'smoking',
          title: 'Можно курить на балконе',
          order: 2,
          primary: true,
        },
        {
          id: '3',
          name: 'cats',
          title: 'Можно с животными',
          order: 3,
          primary: true,
        },
        {
          id: '4',
          name: 'buhlo',
          title: 'Можно бухать',
          order: 4,
          primary: true,
        },
      ],
      filters: {
        houseType: [],
        options: [],
        rules: [],
      },
      advancedFiltersShow: false,
    }
  },
  computed: {
    filterCount() {
      return this.filters.options.length + this.filters.houseType.length
    },
  },
  methods: {
    compareOptionValue(val) {
      console.log(val)
      return val
    },
  },
}
</script>

<style lang="scss" scoped>
.app-bar {
  height: 90px !important;
  margin-top: 90px !important;
  padding: 17px 0 !important;
  color: #37373a !important;
}

.full_search__panel__select--house-types {
  max-width: 450px;
  /*width: 25%;*/
}
.advanced_filters__v-chip.advanced_filters__house_type {
  width: 150px;
  text-align: center;
  justify-content: center;
}

.vertical-separator {
  width: 2px !important;
}

@media (max-width: 1143px) {
  .filter-group {
    width: 50vw;
  }
}

@media (max-width: 794px) {
  .app-bar {
    flex-direction: row;
    justify-content: center;
    height: 60px !important;
    margin-top: 60px !important;
    padding: 0 12px 16px !important;

    &,
    & > * {
      width: 100vw !important;
      min-width: 100vw !important;
      max-width: 100vw !important;
    }
  }

  .filter-group,
  .full_search__panel__select--house-types,
  .vertical-separator {
    display: none;
  }

  .all-filters__btn {
    display: inline-flex;
    width: 91.6vw !important;
    max-width: 91.6vw !important;
    height: 32px !important;
    margin: 0 !important;
    font-size: 14px !important;

    & * {
      font-size: 18px;
    }
  }
}
</style>
