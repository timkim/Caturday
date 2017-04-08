<template>
  <ul v-bind:style="catListStyle">
    <li class="cat-container" v-for="item in items" v-bind:style="catItemStyle">
      <Cat v-bind:message=item.src></Cat>
    </li>
  </ul>
</template>

<script>
  import Cat from './Cat';

  export default {
    name: 'Loved',
    components: {
      'Cat': Cat
    },
    data () {
      return {
        title: 'Loved',
        catItemStyle: {
          listStyle: 'none'
        },
        catListStyle: {
          'padding-left': 0
        },
        items: this.$store.getters.getLovedCats.lovedCats
      };
    },
    mounted () {
    }
  };
</script>
