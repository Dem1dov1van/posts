<template>
    <a-range-picker
      :placeholder="['От', 'До']"
      :separator="'~'"
      :format="dateFormatList"
      suffix-icon=""
      @change="(a, b) => $emit('changeDate', b)"
    />
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  setup() {
    const dateFormatList = ["DD/MM/YYYY", "DD/MM/YYYY"];
    return {
      dateFormatList,
    };
  },
});
</script>
