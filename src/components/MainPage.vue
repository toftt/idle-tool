<template>
  <div>
    <SearchInput
      v-model="searchQuery"
    />
    <ResultGrid
      :results="filteredHeroes"
    />
  </div>
</template>

<script>
import Fuse from 'fuse.js';
import take from 'lodash/take';

import SearchInput from './SearchInput';
import ResultGrid from './ResultGrid';

import heroes from '../data/heroes.json';

// const options = {
//   keys: [
//     {
//       name: 'name',
//       weight: 0.5,
//     },
//     {
//       name: 'faction',
//       weight: 0.5,
//     },
//   ],
// };

const options = { keys: ['name'] };

const fuse = new Fuse(heroes.data, options);

export default {
  name: 'MainPage',
  components: {
    SearchInput,
    ResultGrid,
  },
  data: function () {
    return {
      searchQuery: '',
      heroes: heroes.data,
    };
  },
  computed: {
    filteredHeroes: function () {
      if (!this.searchQuery) return this.heroes;

      const filtered = fuse.search(this.searchQuery);
      return take(filtered, 100);
    },
  },
};
</script>
