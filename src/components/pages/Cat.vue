<template>
  <f7-block inner>
    <img v-bind:src=message />
  </f7-block>
</template>

<script>
  export default {
    name: 'Cat',
    props: ['message']
  };
</script>
