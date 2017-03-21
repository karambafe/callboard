<template>
    <div class="squad__item" :class="{ 'squad__item_active': state }" v-on:click="onClick()">
      {{ name }}
    </div>
</template>

<script>
  export default {
    name: 'squad',
    data() {
      return {
        active: false,
      };
    },
    props: {
      name: String,
      state: Boolean,
      id: Number,
    },
    methods: {
      onClick: function () {
        this.$emit('removestyles', this.id);
      }
    }
  };
</script>

