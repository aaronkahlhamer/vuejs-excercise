<template>
  <div id="app">
    <h1>Tell Us More About You</h1>
    <div class="myform">
      <json-forms
        v-bind:data="data"
        v-bind:renderers="renderers"
        v-bind:schema="schema"
        v-bind:uischema="uischema"
        @change="onChange"
      />
      <button @click="submit" v-bind:disabled="!validationPassed">
        Submit
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { JsonForms, JsonFormsChangeEvent } from "@jsonforms/vue2";
import {
  defaultStyles,
  mergeStyles,
  vanillaRenderers,
} from "@jsonforms/vue2-vanilla";
import schema from "./assets/data/schema.json";
import uischema from "./assets/data/uischema.json";

// mergeStyles combines all classes from both styles definitions
const myStyles = mergeStyles(defaultStyles, { control: { label: "mylabel" } });

const renderers = [
  ...vanillaRenderers,
  // here you can add custom renderers
];

export default defineComponent({
  name: "App",
  components: {
    JsonForms
  },
  data() {
    return {
      // freeze renderers for performance gains
      renderers: Object.freeze(renderers),
      data: {
        fullName: "",
        telephone: "",
        description: "",
        interest: "",
      },
      schema: schema,
      uischema: uischema,
      validationPassed: false,
    };
  },
  methods: {
    isEmpty(value: any) {
      for (let prop in value) {
        if (!value[prop]) return (this.validationPassed = false);
      }
      return (this.validationPassed = true);
    },
    onChange(event: JsonFormsChangeEvent) {
      this.data = event.data;
    }
      this.isEmpty(this.data);
    },
    submit() {
      this.validationPassed
        ? (this.modalVisible = true)
        : (this.modalVisible = false);
    },
  },
});
</script>
