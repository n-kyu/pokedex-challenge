<template>
  <div>
    <Header />
    <SearchPokemon @search_PokeIdName="getPokemons" />
    <PokemonList :pokemons="pokemons" :text="text" v-show="!loading" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import Header from "./components/Header.vue";
import PokemonList from "./components/PokemonList.vue";
import SearchPokemon from "./components/SearchPokemon.vue";

import type { IPokemon, IEvolutionChain } from "./interface/interface";

export default defineComponent({
  name: "App",
  methods: {
    async getPokemons(name: string): Promise<string | void> {
      if (name === "") return;

      this.loading = true;
      this.pokemons = [];

      const species_url = `https://pokeapi.co/api/v2/pokemon-species/${name.toLocaleLowerCase()}/`;

      const pokemon: IPokemon | number = await this.searchDatabase(species_url);

      if (typeof pokemon === "number") {
        this.loading = false;
        return;
      }

      const pokeEvo = pokemon.evolution_chain.url;

      const evoReq = await fetch(pokeEvo);

      const evoData = await evoReq.json();

      await this.recursiveRequests([evoData.chain]);

      await this.getStats();

      this.loading = false;
    },
    async searchDatabase(url: string): Promise<IPokemon | number> {
      const res = await fetch(url);

      if (res.status === 404) {
        this.text = "Não foi possível encontrar o seu pokémon, tente novamente";
        return res.status;
      }

      const data = await res.json();

      return data;
    },
    async recursiveRequests(arr: IEvolutionChain[]) {
      if (arr.length === 0) return;

      for (let i = 0; i < arr.length; i++) {
        const obj = arr[i];

        if (!obj) continue;

        const evolvesTo = obj.evolves_to;

        const url = obj.species.url;

        const pokemon = await this.searchDatabase(url);

        if (typeof pokemon === "number") return;

        this.pokemons.push(pokemon);

        if (evolvesTo.length === 0) continue;
        this.recursiveRequests(evolvesTo);
      }
    },
    async getStats(): Promise<void> {
      const url = "https://pokeapi.co/api/v2/pokemon/";

      for (let poke of this.pokemons) {
        const res = await fetch(url + poke.name);

        const data = await res.json();

        poke.stats = data.stats;
        poke.sprites = data.sprites;
        poke.types = data.types;
      }

      console.log(this.pokemons);
    },
  },
  components: {
    Header,
    SearchPokemon,
    PokemonList,
  },
  data() {
    return {
      pokemons: [] as IPokemon[],
      loading: false,
    };
  },
});
</script>

<style lang="scss">

</style>

