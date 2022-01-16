<template>
  <div>
    <div class="d-flex justify-content-end me-5">
      <button class="btn btn-primary" title="addUser" @click="toAdd">
        <i class="fas fs-3 fa-user-plus"></i>
      </button>
      <button class="btn btn-danger ms-2" title="deleteAll" @click="deleteAll">
        <i class="fas fa-trash-alt me-2"></i>Delete All
      </button>
    </div>
    <List :employee_list="employee_list" @delete="deletee($event)"></List>
  </div>
</template>

<script>
import List from "../components/List";
import axios from "axios";
export default {
  components: {
    List,
  },
  data() {
    return {
      employee_list: [],
    };
  },
  methods: {
    deleteAll() {
      axios
        .delete("https://testing-api-mock.herokuapp.com/users")
        .then(() => {
          this.employee_list = []
        })
        .catch((err) => {
          console.log(err);
        });
    },
    deletee(id) {
      console.log(id);
      this.employee_list = this.employee_list.filter((emp) => {
        return emp.id != id;
      });
    },
    toAdd() {
      this.$router.push("/add");
    },
  },
  mounted() {
    axios
      .get("https://testing-api-mock.herokuapp.com/users")
      .then((res) => {
        console.log(res.data.results);
        return res.data.results;
      })
      .then((data) => {
        this.employee_list = data;
      });
  },
};
</script>

<style>
.circle {
  border-radius: 50%;
}
</style>