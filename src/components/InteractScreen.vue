<template>
  <div class="screen">
    <h1>Interact Components</h1>
    <CardFlip
      v-for="(card, index) in cardContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
    />
  </div>
</template>
<script>
import CardFlip from "@/components/CardConfig.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: { CardFlip },
};
</script>