<template>
  <button class="square" @click="$emit('click')">{{ value }}</button>
</template>

<script>
export default {
  props: ['value']
};
</script>
