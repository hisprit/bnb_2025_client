<template>
  <q-input v-model="model" :mask="mask"></q-input>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "InputPhone",
  emits: ["update:model-value"],
  props: {
    modelValue: { type: String, required: true },
  },
  data() {
    return {};
  },
  computed: {
    model: {
      set(val) {
        this.$emit("update:model-value", val);
      },
      get() {
        return this.modelValue;
      },
    },
    mask() {
      const val = this.modelValue.replace(/[^\d]/g, "");
      let mask = "###-####-####";
      if (val[0] != "0") {
        //0으로 시작하지 않음 1588-1588
        mask = val.length < 8 ? "###-####" : "####-####";
      } else if (val[1] == "2") {
        // 02시작 02-333-3333 02-3333-3333
        mask = val.length < 10 ? "##-###-####" : "##-####-####";
      } else {
        // 050이런거 050-3333-3333
        if (val.startsWith("050")) {
          mask = "####-####-####";
        } else {
          mmask = val.length < 11 ? "###-###-####" : "###-####-####";
        }
      }
      return mask;
    },
  },
});
</script>

<style lang='scss' scoped>
</style>
