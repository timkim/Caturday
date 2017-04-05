<template>
  <div>
    <!-- Scrollable page content-->
    <f7-block-title>{{ title }}</f7-block-title>
    <f7-block inner>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      Distinctio est aliquam officiis quaerat placeat, cum explicabo magni
      soluta totam maxime autem minima accusamus eos suscipit dignissimos
      corporis modi voluptatum fugiat!
    </f7-block>
  </div>
</template>

<script>
  export default {
    name: 'Services',
    data () {
      return {
        title: 'Services Page'
      };
    },
    mounted () {
      this.$$ = this.Dom7;
      var that = this;
      this.$$('#services').on('tab:show', function () {
        that.$$('.infinite-scroll-preloader').remove();
      });
    }
  };
</script>
