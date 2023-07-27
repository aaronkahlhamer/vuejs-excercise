<template>
  <dialog v-bind:open="modalVisible">
    <form method="dialog">
      <div>
        <h1>Hello {{ fullName }}!</h1>
        <p>
          Brace yourself for the most epic phone call of your life at
          {{ telephone }}. We can't wait to chat about your wild and crazy
          interest in {{ interest }}! And trust me, when we start discussing "{{
            description
          }}", it's going to be more entertaining than a circus full of clowns
          on unicycles! Get ready for a rollercoaster of laughter and
          excitement!
        </p>
      </div>
      <button type="submit" v-on:click="closeModal" autofocus>close</button>
    </form>
  </dialog>
</template>

<script lang="ts">
export default {
  props: ["fullName", "telephone", "interest", "description", "modalVisible"],
  methods: {
    closeModal() {
      this.$emit("update:modalVisible", false);
    },
  },
};
</script>
