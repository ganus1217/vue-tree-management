<template>
  <div>
    <input
      type="text"
      :value="value"
      @input="$emit('input', $event.target.value)"
      ref="filter"
    />
  </div>
</template>

<script>
export default {
  name: "FilterComponent",
  props: {
    value: String,
  },
};
</script>