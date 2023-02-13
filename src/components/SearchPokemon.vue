<template>
  <section class="container">
    <img
      alt="Pokemon squirtle gif"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/7.gif"
      class="poke_gif"
    />
    <form @submit="onSubmit">
      <input
        type="text"
        name="PokeIdName"
        v-model="PokeIdName"
        placeholder="Procurar por nome ou ID"
      />
      <BtnComp :text="'Buscar'" type="submit" />
    </form>
    <img
      alt="Pokemon pikachu gif"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/25.gif"
      class="poke_gif"
    />
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BtnComp from "./Button.vue";

export default defineComponent({
  name: "SearchBar",
  data() {
    return {
      PokeIdName: "",
    };
  },
  components: {
    BtnComp,
  },
  methods: {
    onSubmit(e: Event) {
      e.preventDefault();
      this.$emit("search_PokeIdName", this.PokeIdName);
    },
  },
});
</script>

<style scoped lang="scss">
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;

  @media (max-width: 450px) {
    flex-direction: column;
  }
}
.container {
  width: 100%;
  padding: 2rem 0;

  @include flex-center();
  background-color: rgb(37, 57, 107);
  .poke_gif {
    margin: 10px;
  }

  form {
    width: 50%;
    gap: 8px;
    @include flex-center();

    @media (max-width: 767px) {
      width: 100%;
    }
    input {
      width: 100%;
      padding: 0.6rem;
      border: none;
      border-radius: 6px;
      color: #2c3e50;
      font-size: 1.2rem;
    }
  }
  @media (max-width: 450px) {
    padding: 2rem 1rem;
  }
}
</style>
