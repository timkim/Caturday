<template>
  <f7-block>
    <img v-bind:src=message v-on:click.once="like" v-bind:style="catImgStyle" />
  </f7-block>
</template>

<script>
  export default {
    name: 'Cat',
    props: ['message'],
    data: function () {
      return {
        catImgStyle: {
          margin: '0 auto',
          width: '90%'
        },
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
