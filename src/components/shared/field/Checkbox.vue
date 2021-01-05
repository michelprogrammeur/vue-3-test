<template>
  <fieldset>
    <label v-if="label" :for="`checkbox-${name}`">{{ label }}</label>
    <input
      :id="`checkbox-${name}`"
      type="checkbox"
      :checked="checked"
      :name="name"
      :disabled="isDisabled"
      @change="handleChange($event)"
    />
  </fieldset>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
  name: "Checkbox",
  model: {
    value: "checked",
    event: "change"
  },
  props: {
    checked: {
      type: Boolean as PropType<boolean>,
      default: false
    },
    name: {
      type: String as PropType<string>,
      default: "input-text"
    },
    label: {
      type: String as PropType<string>,
      default: null
    },
    isDisabled: {
      type: Boolean as PropType<boolean>,
      default: false
    }
  },
  emits: ["update:checked"],

  setup(props, { emit }) {
    const handleChange = (event: any) => {
      emit("update:checked", event.target.checked);
    };

    return { handleChange };
  }
});
</script>
