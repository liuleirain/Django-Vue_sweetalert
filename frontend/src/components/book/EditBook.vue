<template>
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>编辑列表</h2>
      </div>
    </div>

    <div class="row">
      <div class="col">
        <div class="card">
          <div class="card-body">
            <form @submit.prevent="onSubmit">
              <div class="form-group row">
                <label for="title" class="col-sm-2 col-form-label">标题</label>
                <div class="col-sm-6">
                  <input
                    type="text"
                    placeholder="标题"
                    name="title"
                    class="form-control"
                    v-model.trim="form.title"
                  />
                </div>
              </div>
              <div class="form-group row">
                <label for="description" class="col-sm-2 col-form-label">描述</label>
                <div class="col-sm-6">
                  <textarea
                    type="text"
                    placeholder="描述"
                    name="description"
                    class="form-control"
                    rows="3"
                    v-model.trim="form.description"
                  />
                </div>
              </div>

              <div class="rows">
                <div class="col text-left">
                  <b-button type="submit" variant="primary">编辑</b-button>
                  <b-button type="submit" class="btn-large-space" :to="{ name: 'ListBook' }">取消</b-button>
                </div>
              </div>
            </form>
          </div>
        </div>
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
      form: {
        title: "",
        description: ""
      }
    };
  },
  methods: {
    onSubmit() {
      axios
        .put(this.path, this.form)
        .then(res => {
          this.form.title = res.data.title;
          this.form.description = res.data.description;
          swal("更新成功!", "", "success").catch(err => console.log(err));
        })
        .catch(err => swal("更新失败!", "", "err"));
    },
    getBook() {
      axios
        .get(this.path)
        .then(res => (this.form = res.data))
        .catch(err => swal("更新失败!", "", "err"));
    }
  },
  created() {
    this.getBook();
  }
};
</script>

<style></style>
