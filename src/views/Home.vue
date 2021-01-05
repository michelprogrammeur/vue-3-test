<template>
  <div class="home">
    <form @submit="handleFormSubmit">
      <text-field
        v-model.trim.capitalize="form.firstname"
        name="firstname"
        label="Nom"
      />

      <text-field
        v-model.trim.capitalize="form.lastname"
        name="lastname"
        label="Prénom"
      />

      <checkbox
        v-model:checked="form.newsletter"
        name="newsletter"
        label="Souscrire au newsletter"
      />

      <button type="submit">
        Submit
      </button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import TextField from "@/components/shared/field/TextField.vue";
import Checkbox from "@/components/shared/field/Checkbox.vue";

interface FormUserTypeInterface {
  firstname: string | null;
  lastname: string | null;
  newsletter: boolean;
}

export default defineComponent({
  name: "Home",
  components: { Checkbox, TextField },

  setup() {
    const form: FormUserTypeInterface = reactive({
      firstname: "toto",
      lastname: null,
      newsletter: false
    });

    const handleFormSubmit = () => {
      console.log("submit");
    };

    return {
      form,
      handleFormSubmit
    };
  }
});
</script>
