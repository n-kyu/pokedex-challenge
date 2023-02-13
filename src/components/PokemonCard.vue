<template>
  <article
    :style="{ borderColor: pokemon.color.name }"
    :class="{ showInfo: showInfo }"
    @click="showInfo = !showInfo"
  >
    <div class="sprite_name">
      <div class="sprite_img">
        <img
          :src="pokemon?.sprites?.other?.dream_world?.front_default"
          :alt="pokemon.name"
        />
      </div>
      <h3>
        {{ pokemon.name.slice(0, 1).toUpperCase() + pokemon.name.slice(1) }}
      </h3>
    </div>
    <div v-if="showInfo" class="info">
      <ul class="more_info">
        <li v-if="pokemon.habitat">
          Habitat:
          <span>{{
            pokemon.habitat.name.slice(0, 1).toUpperCase() +
            pokemon.habitat.name.slice(1)
          }}</span>
        </li>
      </ul>
      <ul class="stats">
        <li>
          HP: <span>{{ pokemon?.stats[0]?.base_stat }}</span>
        </li>
        <li>
          SPD: <span>{{ pokemon?.stats[5]?.base_stat }}</span>
        </li>
        <li>
          ATK: <span>{{ pokemon?.stats[1]?.base_stat }}</span>
        </li>
        <li>
          DEF: <span>{{ pokemon?.stats[2]?.base_stat }}</span>
        </li>
        <li>
          SpATK: <span>{{ pokemon?.stats[3]?.base_stat }}</span>
        </li>
        <li>
          SpDEF: <span>{{ pokemon?.stats[4]?.base_stat }}</span>
        </li>
      </ul>
      <ul class="types">
        <li v-for="elemental in pokemon?.types" :key="elemental.type.url">
          {{
            elemental.type.name.slice(0, 1).toUpperCase() +
            elemental.type.name.slice(1)
          }}
        </li>
      </ul>
    </div>
  </article>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "PokeCard",
  props: ["pokemon"],
  data() {
    return {
      showInfo: false,
    };
  },
});
</script>

<style scoped lang="scss">
article {
  max-width: 300px;
  padding: 1.2rem 2rem;
  background: white;
  border: 2px solid;

  &:hover {
    cursor: pointer;
    box-shadow: 2px 2px 3px -1px #3335;
  }

  @media (max-width: 500px) {
    max-width: initial;
    width: 100%;
  }

  .sprite_name {
    div {
      margin: 0;
      overflow: hidden;
      img {
        width: 100%;
        height: 350px;

        @media (max-width: 500px) {
          height: auto;
        }
      }
    }

    position: relative;
    z-index: 1;
  }

  @mixin ul-style {
    max-width: 300px;
    width: 100%;
    margin: 0;
    padding: 0;
    list-style: none;
  }

  @mixin flex-space-between {
    display: flex;
    justify-content: space-between;
  }

  .info {
    @include flex-space-between();
    flex-direction: column;
    gap: 0.5rem;
  }
  .stats {
    @include ul-style();

    @include flex-space-between();
    flex-wrap: wrap;

    li {
      width: 45%;
      text-align: left;
      font-weight: 700;
      @include flex-space-between();

      span {
        font-weight: 400;
      }
    }
  }

  .body,
  .types {
    @include ul-style();

    gap: 1rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    li {
      width: 45%;
      font-weight: 700;
    }
  }

  .more_info {
    @include ul-style();

    li {
      @include flex-space-between();

      font-weight: 700;

      span {
        font-weight: 400;
      }
    }

    li:nth-child(2) {
      span {
        font-size: 0.85rem;
      }
    }
  }
}
</style>
