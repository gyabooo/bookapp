<template>
    <div>
      <h3 class="title">タイトルで検索してください</h3>
      
      <div class="field">
        <div class="control">
          <div class="error">{{ error }}</div>
        </div>
      </div>

      <div class="field has-addons">
        <div class="control">
          <input class="input" type="text" v-model="keyword">
        </div>
        <div class="control">
          <button class="button is-info" @click="search">検索</button>
        </div>
      </div>

      <div class="columns is-multiline">
        <book v-for="book in this.books" :key="book.id" :book="book"></book>
      </div>
    </div>
</template>

<script>
import Book from '~/components/Book.vue'

const convert = require('xml-js');
const axios = require('axios');
// let path = 'http://localhost:3000/api/sru?operation=searchRetrieve&maximumRecords=10&query=title%3d%22%e6%a1%9c%22%20AND%20from=%222018%22';
// let path = '/api/sru?operation=searchRetrieve&maximumRecords=10&query=title%3d%22%e6%a1%9c%22%20AND%20from=%222018%22';
// let path = '/api/opensearch?cnt=20&title=マリーアントワネット&ndc=2&dpid=iss-ndl-opac'
let path = 'https://iss.ndl.go.jp/api/opensearch?cnt=20&title='

export default {
  components: {
    Book
  },
  data: function() {
    return {
      keyword: '',
      books: [],
      error: ''
    }
  },
  methods: {
    search: function() {
      this.error = '';
      this.books.splice(0, this.books.length);

      axios
        .get(path + this.keyword)
        .then(res => {
          this.books = convert.xml2js(res.data, {ignoreComment: true, alwaysChildren: true})
                        .elements[0].elements[0].elements
                        .filter(element => element.name === 'item');
        })
        .catch(e => {
          this.error = e.message;
        })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
