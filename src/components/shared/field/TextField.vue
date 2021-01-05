<template>
  <fieldset>
    <label v-if="label" :for="`input-${name}`">{{ label }}</label>
    <input
      :id="`input-${name}`"
      :value="modelValue"
      :name="name"
      :disabled="isDisabled"
      type="text"
      @input="handleInput($event)"
    />
  </fieldset>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

interface VModelModifierInterface {
  trim?: boolean;
  lazy?: boolean;
  capitalize?: boolean;
}

export default defineComponent({
  name: "TextField",
  props: {
    modelValue: {
      type: String as PropType<string>,
      default: null
    },
    modelModifiers: {
      default: (): VModelModifierInterface => ({ capitalize: false })
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
  emits: ["update:modelValue"],

  setup(props, { emit }) {
    const handleInput = (event: any) => {
      let value: string = event.target.value;
      const modifier: VModelModifierInterface = props.modelModifiers;
      if (modifier.capitalize) {
        value = value.charAt(0).toUpperCase() + value.slice(1);
      }

      emit("update:modelValue", value);
    };

    return { handleInput };
  }
});
</script>
