<template>
  <div>
    <div class="header-t">
      <img v-bind:src="require('../assets/logo_pie_susuerte.png')" class="logo-susuerte" alt="">
      <h1>Usuarios</h1>
    </div>
    <div class="content-table">
      <v-data-table
        :headers="headers"
        :items="Users"
        :items-per-page="5"
        class="elevation-1 table"
      ></v-data-table>
    </div>
  </div>
</template>
<script>
import "../styles/userTable.css";
import axios from "axios";
export default {
  name: "userTable",
  data() {
    return {
      headers: [
        {
          text: "Nombre Completo",
          value: "name",
        },
        { text: "Genero", value: "gender" },
        { text: "Pais", value: "country" },
        { text: "email", value: "email" },
        { text: "Telefono", value: "phone" },
      ],
      Users: [],
    };
  },
  computed: {},
  async created() {
    for (var i = 0; i < 6; i++) {
      axios.get("https://randomuser.me/api/").then((result) => {
        let user = {};
        user.name =
          result.data.results[0].name.first +
          " " +
          result.data.results[0].name.last;
        user.country = result.data.results[0].location.country;
        user.gender = result.data.results[0].gender;
        user.email = result.data.results[0].email;
        user.phone = result.data.results[0].phone;
        this.Users.push(user);
      });
    }
  },
  mounted() {},
  methods: {},
  components: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
