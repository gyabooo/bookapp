<template>
  <div class="column is-4 book-content">
    <div class="card">
      <div class="card-header">
        <div class="card-header-title">{{ title }}</div>
      </div>
      <div class="card-image">
        <figure class="image is-1by1">
          <a :href="link" target="_blank"><img :src="image" alt="画像"></a>
        </figure>
      </div>
      <div class="card-content" v-html="description"></div>
    </div>
  </div>
</template>

<script>
const axios = require('axios');
let path = '/thumbnail/';
let no_image_path = '/no-image.png';

export default {
  props: ['book'],
  data: function () {
    return {
      image: 'https://iss.ndl.go.jp/',
      title: this.book.elements.filter(v => v.name === 'title')[0].elements[0].text,
      description: this.book.elements.filter(function(el){ if(el.name === "description") return true } )[0].elements[0].cdata,
      link: this.book.elements.filter(function(el){ if(el.name === "link") return true } )[0].elements[0].text
    }
  },
  created: function() {
    let isbn = this.book.elements.filter(function(el){ if(el.name === "dc:identifier" && el.attributes['xsi:type'] === 'dcndl:ISBN') return true } )
    let image_path = '';

    if (isbn.length === 0) {
      this.image = no_image_path;
      return true;
    }

    axios
      .get(path + isbn[0].elements[0].text)
      .then(res => {
        this.image = this.image + path + isbn[0].elements[0].text;
      })
      .catch(e => {
        this.image = no_image_path;
      })
  }
}
</script>

<style scoped>
.book-content {
  margin-bottom: 40px;
}
</style>