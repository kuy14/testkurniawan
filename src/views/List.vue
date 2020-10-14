<template>
  <div>
    <h1>List</h1>
    <button @click="getlist">Lihat List</button>
    <input v-model="listname" placeholder="Masukkan list" />
    <button @click="addlist">Tambah List</button>
    <h5>Data List</h5>
    <ul id="datalist">
      <li v-for="item in items" :key="item.name">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "List",
  data() {
    return {
      listname: "",
      items: [],
    };
  },
  methods: {
    addlist() {
      const config = {
        headers: {
          Authorization: `Bearer ${"eyJhbGciOiJIUzUxMiJ9.eyJyb2xlcyI6W119.i2OVQdxr08dmIqwP7cWOJk5Ye4fySFUqofl-w6FKbm4EwXTStfm0u-sGhDvDVUqNG8Cc7STtUJlawVAP057Jlg"}`,
        },
      };
      const bodyParameters = {
        name: this.listname,
      };

      axios
        .post("http://18.139.50.74:8080/checklist", bodyParameters, config)
        .then((response) => {
          alert(response.data.message);
        })
        .catch(console.log);
    },
    getlist() {
      axios
        .get("http://18.139.50.74:8080/checklist", {
          headers: {
            Authorization: `Bearer ${"eyJhbGciOiJIUzUxMiJ9.eyJyb2xlcyI6W119.i2OVQdxr08dmIqwP7cWOJk5Ye4fySFUqofl-w6FKbm4EwXTStfm0u-sGhDvDVUqNG8Cc7STtUJlawVAP057Jlg"}`,
          },
        })
        .then((res) => {
          console.log(res.data.data);
          this.items = res.data.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
