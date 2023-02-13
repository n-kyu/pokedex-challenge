<template>
  <button @click="onClick()">
    <svg
      stroke="currentColor"
      fill="currentColor"
      stroke-width="0"
      viewBox="0 0 24 24"
      height="20"
      width="20"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path fill="none" d="M0 0h24v24H0z"></path>
      <path
        d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"
      ></path>
    </svg>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "BtnComp",
  props: {
    text: String,
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
});
</script>

<style scoped lang="scss">
button {
  padding: 10px;
  color: #fff;
  font-size: 1.2rem;
  border: none;
  border-radius: 6px;
  background-color: rgb(255, 165, 0);

  &:hover {
    cursor: pointer;
    background-color: rgb(42, 117, 187);
  }
  
  @media (max-width: 450px) {
      width: 100%;
    }
}
</style>
