<template>
  <ul>
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
        items: this.$store.getters.getLovedCats.lovedCats
      };
    },
    mounted () {
    }
  };
</script>
