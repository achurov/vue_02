<template>
  <div class="container column">
    <cv-form @add="add"></cv-form>
    <cv-card></cv-card>
  </div>
  <comments></comments>
</template>

<script>
import Comments from "./components/Comments.vue";
import CVCard from "./components/CVCard.vue";
import CVForm from "./components/CVForm.vue";

export default {
  data(){
    return {
      data: []
    }
  },
  provide() {
    return {
      data: this.data,
    };
  },
  methods:{
    add(item) {
      this.data.push(item)
    },
  },
  components: {
    "cv-form": CVForm,
    "cv-card": CVCard,
    comments: Comments,
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
