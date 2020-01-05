<template>
    <div>
      <h3 class="title">タイトルを入力してください</h3>
      
      <div class="field">
        <div class="control">
          <div class="error">{{ error }}</div>
        </div>
      </div>

      <div class="field has-addons">
        <div class="control is-expanded">
          <input class="input" type="text" v-model="keyword">
        </div>
        <div class="control">
          <button class="button is-info" @click="search">検索</button>
        </div>
      </div>

      <loading :class="{'is-hidden': !isSearch}"></loading>

      <div class="columns is-multiline">
        <book v-for="book in this.books" :key="book.id" :book="book"></book>
      </div>
    </div>
</template>

<script>
import Book from '~/components/Book.vue'
import Loading from '~/components/Loading.vue'

const axios = require('axios');
let path = '/.netlify/functions/search?title='

export default {
  components: {
    Book,
    Loading
  },
  data: function() {
    return {
      keyword: '',
      books: [],
      error: '',
      isSearch: false
    }
  },
  methods: {
    search: function() {
      this.error = '';
      this.isSearch = true;
      this.books.splice(0, this.books.length);

      axios
        .get(path + this.keyword)
        .then(res => {
          this.books = res.data.content;
        })
        .catch(e => {
          this.error = e.message;
        })
        .finally(() => {
          if(this.books.length === 0) {
            this.error = '検索結果が0件です'
          }
          this.isSearch = false;
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.search-box {
  width: 90vw;
}
</style>
