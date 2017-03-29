<template>
  <ul>
    <li v-for="item in items">
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
      function encodeQueryData (data) {
        let ret = [];
        for (let d in data) {
          ret.push(encodeURIComponent(d) + '=' + encodeURIComponent(data[d]));
        }
        return ret.join('&');
      }

      var query = {
        'q': 'cat',
        'limit': 10,
        'rating': 'g',
        'api_key': 'dc6zaTOxFJmzC'
      };

      var queryString = encodeQueryData(query);
      var that = this;
      fetch('http://api.giphy.com/v1/gifs/search?' + queryString).then(function (response) {
        return response.json();
      }).then(function (json) {
        for (var img in json.data) {
          that.items.push({'src': json.data[img].images.downsized.url});
        }
      }).catch(function (err) {
        if (err) {
          console.log(err.stack);
        }
      });
    }
  };
</script>
