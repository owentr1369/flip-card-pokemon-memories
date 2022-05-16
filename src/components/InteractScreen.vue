<template>
  <div class="screen">
    <h1>Interact Components</h1>
    <CardFlip
      v-for="(card, index) in cardContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="checkRule($event)"
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
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      this.rules.push(card);

      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("right");
        this.rules = [];
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("wrong");
        setTimeout(() => {
          // Close 2 card
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // console.log(this.$refs[`card-${this.rules[0].index}`][0]);

          // Reset rules to []
          this.rules = [];
        }, 1000);
      } else {
        return false;
      }
    },
  },
};
</script>