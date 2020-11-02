<template>
  <div>
    <v-text-field :label="label" :name="name" :id="`input-${name}`" @input="handleInput" :required="required" :type="type" :value="initialValue" :placeholder="placeholder"></v-text-field>
    <b-form-invalid-feedback v-if="stateError">
        <span>{{ messageError}}</span>
      </b-form-invalid-feedback>
  </div>
</template>

<script>
export default {
  props:{
    value: {
      type: String,
      default: ""
    },
    label:{
      type: String,
    },
    description: {
      type: String
    },
    type: {
      type: String,
      default: 'text'
    },
    placeholder: {
      type: String,
    },
    name: {
      type: String,
      required: true
    },
    required: {
      type: String,
    },
    stateError: {
      type: Boolean,
      default: null
    },
    messageError: {
      type: String
    },
  },
  data() {
    return {
      size: "",
      initialValue: this.value
    }
  },
  methods: {
    handleInput(e)
    {
      this.$emit("input", e);
    },
  },
}
</script>
