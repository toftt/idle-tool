<template>
  <div class="grid">
    <div
    v-for="hero in results"
    :key="hero.name"
    @click="addHero(hero)"
    >
    <img :src="hero.imageUrl" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ResultGrid',
  props: {
    results: Array,
  },
  methods: {
    addHero: function (hero) {
      this.$emit('addHero', hero);
    },
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  max-width: 600px;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
}
</style>
