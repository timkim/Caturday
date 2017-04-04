<template>
  <ul>
    <li class="cat-container" v-for="item in items">
      <Cat v-bind:message=item.src></Cat>
    </li>
  </ul>
</template>

<script>
  import Cat from './Cat';

  export default {
    name: 'Cats',
    components: {
      'Cat': Cat
    },
    data: function () {
      return {
        items: []
      };
    },
    methods: {
      updateItems: function (item) {
        this.items.push(item);
      }
    },
    mounted () {
      var loading = false;

      function encodeQueryData (data) {
        let ret = [];
        for (let d in data) {
          ret.push(encodeURIComponent(d) + '=' + encodeURIComponent(data[d]));
        }
        return ret.join('&');
      }

      function getCats (queryString, items, loading) {
        fetch('http://api.giphy.com/v1/gifs/search?' + queryString).then(function (response) {
          loading = true;
          return response.json();
        }).then(function (json) {
          for (var img in json.data) {
            items.push({'src': json.data[img].images.downsized.url});
          }
          loading = false;
        }).catch(function (err) {
          if (err) {
            console.log(err.stack);
          }
        });
      }

      function queryCats (offset) {
        return encodeQueryData({
          'q': 'cat',
          'limit': 10,
          'offset': offset !== undefined ? offset : 0,
          'rating': 'g',
          'api_key': 'dc6zaTOxFJmzC'
        });
      }
      this.$$ = this.Dom7;

      var that = this;
      this.$$('.infinite-scroll').on('infinite', function () {
        if (!loading) {
          var catQuery = queryCats(that.items.length);
          getCats(catQuery, that.items, loading);
        }
      });

      var catQuery = queryCats();
      getCats(catQuery, this.items, loading);
    }
  };
</script>
