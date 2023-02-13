<template>
  <section>
    <PokemonCard
      :pokemon="pokemon"
      v-show="pokemons.length > 0"
      :key="pokemon.id"
      v-for="pokemon in pokemons"
    />

    <div v-show="pokemons.length === 0">
      <h2>{{ text }}</h2>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PokemonCard from "./PokemonCard.vue";

export default defineComponent({
  name: "PokeList",
  props: ["pokemons", "text"],
  components: { PokemonCard },
});
</script>

<style scoped lang="scss">
section {
  background-color: rgb(42, 117, 187);
  border: 2px solid black;
  padding: 2rem;
  gap: 2rem;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
</style>

