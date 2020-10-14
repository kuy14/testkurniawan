<template>
  <div>
    <h1>List</h1>
    <button @click="getlist">Lihat List</button><br />
    <input
      style="margin-top: 10px;margin-right: 5px;"
      v-model="listname"
      placeholder="Masukkan nama list"
    />
    <button @click="addlist">Tambah List</button>
    <h5>Data List</h5>
    <ul id="datalist" style="list-style-type: none;">
      <li v-for="item in items" :key="item.name" style="margin-bottom: 10px;">
        Nama List : {{ item.name }} |
        <button @click="detaillist(item.id)">Buka List</button> |
        <button @click="dellist(item.id)">Hapus List</button>
      </li>
    </ul>

    <h5>Data Item</h5>
    <ul id="datalist" style="list-style-type: none;">
      <li v-for="item in item" :key="item.name" style="margin-bottom: 10px;">
        Nama Item : {{ item.name }}
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
      item: [],
    };
  },
  mounted: function() {
    this.getlist();
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
          this.getlist();
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
          this.items = res.data.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    dellist(id) {
      console.log(id);
      axios
        .delete("http://18.139.50.74:8080/checklist/" + id, {
          headers: {
            Authorization: `Bearer ${"eyJhbGciOiJIUzUxMiJ9.eyJyb2xlcyI6W119.i2OVQdxr08dmIqwP7cWOJk5Ye4fySFUqofl-w6FKbm4EwXTStfm0u-sGhDvDVUqNG8Cc7STtUJlawVAP057Jlg"}`,
          },
        })
        .then(() => {
          this.getlist();
        })
        .catch((error) => {
          console.error(error);
        });
    },
    detaillist(id) {
      console.log(id);
      axios
        .get("http://18.139.50.74:8080/checklist", {
          headers: {
            Authorization: `Bearer ${"eyJhbGciOiJIUzUxMiJ9.eyJyb2xlcyI6W119.i2OVQdxr08dmIqwP7cWOJk5Ye4fySFUqofl-w6FKbm4EwXTStfm0u-sGhDvDVUqNG8Cc7STtUJlawVAP057Jlg"}`,
          },
        })
        .then((res) => {
          this.item = res.data.data[id - 1].items;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
