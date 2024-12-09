<template>
  <div>
    <label :for="name" class="form-label">{{ label }}</label>
    <input
      :type="type"
      :class="{ 'is-invalid': errors[name] }"
      :value="value"
      :name="name"
      class="form-control"
    />
    <div class="invalid-feedback" v-if="errors[name]">
      {{ errors[name][0] }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: "Input Label",
    },
    type: {
      type: String,
      default: "text",
    },
    name: {
      type: String,
      default: "name",
    },
    errors: {
      type: Object,
    },
    value: {
      default: null,
    },
  },
};
</script>

<style lang="scss" scoped></style>
