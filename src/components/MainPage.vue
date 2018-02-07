<template>
  <div>
    <SearchInput
      v-model="searchQuery"
    />
    <ResultGrid
      :results="filteredHeroes"
      @addHero="addHero"
    />
  </div>
</template>

<script>
import Fuse from 'fuse.js';
import take from 'lodash/take';

import SearchInput from './SearchInput';
import ResultGrid from './ResultGrid';

import heroJson from '../data/heroes.json';

const options = { keys: ['name'] };
const { data: heroData } = heroJson;

const fuse = new Fuse(heroData, options);

export default {
  name: 'MainPage',
  components: {
    SearchInput,
    ResultGrid,
  },
  data: function () {
    const selectedHeroes = heroData.reduce((obj, hero) => {
      obj[hero.name] = 0;
      return obj;
    }, {});

    return {
      searchQuery: '',
      selectedHeroes,
    };
  },
  computed: {
    filteredHeroes: function () {
      if (!this.searchQuery) return heroData;

      const filtered = fuse.search(this.searchQuery);
      return take(filtered, 100);
    },
  },

  methods: {
    addHero: function (hero) {
      this.selectedHeroes[hero.name] += 1;
    },
  },
};
</script>
