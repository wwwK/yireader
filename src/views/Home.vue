<template>
  <div class="home">
    <p v-if="bookInfos.length === 0">请通过右上角搜索框添加书籍。</p>
    <b-container v-else>
      <b-row cols="1">
        <b-col v-for="(bookInfo, index) in bookInfos" :key="index">
          <BookInfo :index="index" :info="bookInfo" :reading="getReading(bookInfo)" :inBookshelf="true" />
        </b-col>
      </b-row>  
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import BookInfo from '@/components/BookInfo.vue'

export default {
  name: 'Home',
  data: function() {
    return {
    };
  },
  created() {
    this.$store.dispatch('fetchAllBook');
  },
  computed: {
    bookInfos() {
      return this.$store.getters.bookInfosInBookshelf;
    },
  },
  methods: {
    getReading(bookInfo) {
      const fullName = bookInfo.name + '-' + bookInfo.author;
      return this.$store.getters.getReadingProcess(fullName);
    }
  },
  components: {
    BookInfo
  },
  title: "易读"
}
</script>
