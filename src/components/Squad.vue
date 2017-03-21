<template>
    <div class="callboard__squad" :class="{ 'callboard__squad_active': state }" v-on:click="onClick()">
      {{ name }}
      {{ state }}
      {{ id }}
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

