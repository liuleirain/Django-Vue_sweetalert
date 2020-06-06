<template>
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>书籍列表</h2>
        <b-button class="mb-3" size="sm" :to="{name: 'NewBook'}">添加书籍</b-button>

        <div class="col-md-12">
          <b-table striped hover :items="books" :fields="fields">
            <template v-slot:cell(action)="data">
              <b-button
                size="sm"
                variant="primary"
                :to="{ name: 'EditBook', params: { bookId: data.item.id } }"
              >编辑</b-button>
              <b-button
                size="sm"
                variant="danger"
                :to="{ name: 'DeleteBook', params: { bookId: data.item.id } }"
              >删除</b-button>
            </template>
          </b-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      fields: [
        { key: "title", label: "标题" },
        { key: "description", label: "描述" },
        { key: "action", label: "" }
      ],
      books: []
    };
  },
  methods: {
    getBooks() {
      const path = "http://localhost:8000/api/v1.0/books/";
      axios
        .get(path)
        .then(res => (this.books = res.data))
        .catch(err => console.log(err));
    }
  },
  created() {
    this.getBooks();
  }
};
</script>

<style></style>
