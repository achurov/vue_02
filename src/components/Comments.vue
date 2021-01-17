<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">
        Загрузить комментарии
      </button>
    </p>
    <div class="loader" v-if="loader"></div>
    <div class="card" v-if="commentsShow">
      <h2>Комментарии</h2>
      <ul class="list">
        <comment
          v-for="item in comments"
          :key="item"
          :email="item.email"
          :body="item.body"
        ></comment>
      </ul>
    </div>
  </div>
</template>

<script>
import Comment from "./Comment.vue";

export default {
  data() {
    return {
      comments: [],
      loader: false,
    };
  },
  computed: {
    commentsShow: function () {
      return this.comments.length > 0;
    },
  },
  methods: {
    async loadComments() {
      this.loader = true;
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/comments?_limit=42",
        {
          method: "GET",
        }
      );

      this.loader = false;
      this.comments = await response.json();
    },
  },
  components: {
    comment: Comment,
  },
};
</script>

<style>
</style>