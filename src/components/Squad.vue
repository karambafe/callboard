<template>
  <md-tab :class="{ 'squad__item_active': state }" :md-active="state" :md-label="name">
  </md-tab>
</template>

<script>
  export default {
    name: 'squad',
    props: {
      name: String,
      state: Boolean,
      id: Number,
    },
  };
</script>

