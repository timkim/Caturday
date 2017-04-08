<template>
  <ul v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="10" v-bind:style="catListStyle">
    <li class="cat-container" v-for="item in items" v-bind:style="catItemStyle">
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
        catItemStyle: {
          listStyle: 'none'
        },
        catListStyle: {
          'padding-left': 0
        },
        catCount: 0,
        busy: false,
        items: []
      };
    },
    methods: {
      encodeQueryData: function (data) {
        let ret = [];
        for (let d in data) {
          ret.push(encodeURIComponent(d) + '=' + encodeURIComponent(data[d]));
        }
        return ret.join('&');
      },
      getCats: function (queryString, items) {
        var that = this;
        this.$$ = this.Dom7;

        if (!this.busy && this.$$('#cats').hasClass('active')) {
          this.catCount += 10;
          this.busy = true;
          fetch('http://api.giphy.com/v1/gifs/search?' + queryString).then(function (response) {
            return response.json();
          }).then(function (json) {
            that.busy = false;
            for (var img in json.data) {
              that.items.push({'src': json.data[img].images.downsized.url});
            }
          }).catch(function (err) {
            if (err) {
              console.log(err.stack);
            }
          });
        }
      },
      queryCats: function (offset) {
        return this.encodeQueryData({
          'q': 'cat',
          'limit': 10,
          'offset': offset !== undefined ? offset : 0,
          'rating': 'g',
          'api_key': 'dc6zaTOxFJmzC'
        });
      },
      updateItems: function (item) {
        this.items.push(item);
      },
      loadMore: function () {
        var catQuery = this.queryCats(this.catCount);
        this.getCats(catQuery, this.items);
      }
    },
    mounted () {
      var catQuery = this.queryCats();
      this.getCats(catQuery, this.items);
    }
  };
</script>
