<template>
  <f7-block inner>
    <img v-bind:src=message v-on:click.once="like" />
  </f7-block>
</template>

<script>
  export default {
    name: 'Cat',
    props: ['message'],
    data: function () {
      return {
        liked: false
      };
    },
    methods: {
      like: function (event) {
        this.$$ = this.Dom7;
        if (this.$$('#cats').hasClass('active')) {
          this.$store.commit('addCat', {'src': event.target.src});
        }
      }
    }
  };
</script>
