<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h3>确认要删除这本书籍相关的信息吗？</h3>
        <p>标题：{{ this.element.title }}</p>
        <p>描述：{{ this.element.description }}</p>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <b-button @click="deleteBook" variant="danger">删除</b-button>
      </div>
    </div>
  </div>
</template> 

<script>
import axios from "axios";
import swal from "sweetalert";

export default {
  data() {
    return {
      path: `http://localhost:8000/api/v1.0/books/${this.$route.params.bookId}/`,
      element: {
        title: "",
        description: ""
      }
    };
  },
  methods: {
    getBook() {
      axios
        .get(this.path)
        .then(res => (this.element = res.data))
        .catch(err => console.log(err));
    },
    deleteBook() {
      axios
        .delete(this.path, this.element)
        .then(() => {
          location.href = "/books";
        })
        .catch(err => swal("没有删除成功！", "", "err"));
    }
  },
  created() {
    this.getBook();
  }
};
</script> 

<style>
</style>