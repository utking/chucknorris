<template>
  <div class="chucknorris">
    <h1>About Chuck Norris:</h1>
    <h2>{{ quote }}</h2>
    <br>

    <a v-on:click="fetchNext" href="#">I want more!</a>
  </div>
</template>

<script>
export default {
  name: 'chucknorris',
  data() {
    return {
      quote: '',
    };
  },
  created() {
    this.fetchNext();
  },
  methods: {
    fetchNext(e) {
      this.quote = 'Wait for it...';
      if (e) {
        e.preventDefault();
      }
      this.$http.get('https://api.chucknorris.io/jokes/random')
      .then((resp) => {
        this.quote = resp.data.value;
      }, () => {
        this.quote = 'Failed to load one :(';
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
a {
  color: #AAA;
  text-decoration: none;
}
a:hover {
  color: #555;
}
</style>
