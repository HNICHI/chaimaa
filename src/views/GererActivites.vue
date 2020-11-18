<template>
  <div>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">
          <i class="fa fa-bar-chart" aria-hidden="true"></i>
          Gérer les activités
        </li>
      </ol>
    </nav>
    <div class="table-crud">
      <!-- table select -->
      <div class="row search-select">
        <div class="input-group data-table col-2">
          <select class="custom-select">
            <option value="1" selected>10</option>
            <option value="2">25</option>
            <option value="3">50</option>
            <option value="3">100</option>
          </select>
        </div>
        <!-- Search form -->
        <form class="search form-inline col-md-3">
          <input
            class="form-control w-75"
            type="text"
            placeholder="Search"
            aria-label="Search"
          />
          <i class="fa fa-search" aria-hidden="true"></i>
        </form>
      </div>
      <!-- button ajouter -->
      <div class="form-row form-ajouter">
        <div class="form-group col-md-3">
          <label for="">Activités</label>
          <select v-model="activite" class="form-control form-control">
            <option>Sélectionnez Activité</option>
            <option
              v-bind:value="activity"
              :key="activity.id_activite"
              v-for="activity in gererAllActivites"
            >
              {{ activity.activite }}
            </option>
          </select>
        </div>
        <div class="form-group col-md-3">
          <label for="">Noms clients</label>
          <!-- <select v-model="nom_client" class="form-control form-control">
            <option>Sélectionnez Nom client</option>
            <option
              v-bind:value="nom_client"
              :key="nom_client.id_client"
              v-for="nom_client in gererAllActivites"
            >
              {{ nom_client.nom_client }}
            </option>
          </select> -->
          <input
            type="string"
            class="form-control"
            v-model="nom_client"
            placeholder="Nom client"
          />
        </div>
        <div class="form-group col-md-3">
          <label for="">Prénoms clients</label>
          <!-- <select v-model="prenom_client" class="form-control form-control">
            <option>Sélectionnez Prénom client</option>
            <option
              v-bind:value="prenom_client"
              :key="prenom_client.id_client"
              v-for="prenom_client in gererAllActivites"
            >
              {{ prenom_client.prenom_client }}
            </option>
          </select> -->
          <input
            type="string"
            class="form-control"
            v-model="prenom_client"
            placeholder="Prénom client"
          />
        </div>
        <div class="button-recherche col-md-3">
          <button type="submit" class="btn btn-light" @click="submit">
            Ajouter
            <i class="fa fa-plus" aria-hidden="true"></i>
          </button>
        </div>
      </div>
      <!-- Table crud -->
      <div class="table-crud-body row">
        <table class="table table-hover col-md-8 m-auto">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nom client</th>
              <th scope="col">Prénom client</th>
              <th scope="col">Activités</th>
              <th scope="col">Filières</th>
              <th scope="col">Secteurs</th>
              <th scope="col">Actions</th>
            </tr>
          </thead>
          <tbody class="crud-body">
            <tr
              :key="activiteClient.id_client"
              v-for="activiteClient in gererAllActivitesClient"
            >
              <th scope="row" class="id-client">
                {{ activiteClient.id_client }}
              </th>
              <td>{{ activiteClient.nom_client }}</td>
              <td>{{ activiteClient.prenom_client }}</td>
              <td>{{ activiteClient.activite }}</td>
              <td>{{ activiteClient.filiere }}</td>
              <td>{{ activiteClient.secteur }}</td>
              <td class="actions-btn">
                <!-- <router-link
                  :to="{
                    name: 'ville',
                    params: { id: ville.id_ville }
                  }"
                  class="show-btn"
                >
                  <i class="fa fa-eye" aria-hidden="true"></i>
                </router-link> -->
                <router-link to="#" class="edit-btn">
                  <i class="fa fa-pencil-square-o" aria-hidden="true"></i>
                </router-link>
                <router-link to="#" class="delete-btn">
                  <i class="fa fa-trash-o" aria-hidden="true"></i>
                </router-link>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <Pagination></Pagination>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
import Pagination from "../components/Layout/Pagination";
export default {
  name: "GererActivites",
  components: {
    Pagination,
  },
  data() {
    return {
      activite: "",
      nom_client: "",
      prenom_client: "",
    };
  },
  methods: {
    submit() {
      let data = new FormData();
      data.append("activityClient", this.activite.id_activite);
      data.append("client", this.nom_client);
      data.append("client", this.prenom_client);
      console.log(this.activite, this.nom_client, this.prenom_client);
      this.errors = {};
      console.log("sending");
      this.$store.dispatch("addActivitesClient", data);
      this.activite = "";
      this.nom_client = "";
      this.prenom_client = "";
    },
    // spread operator
    ...mapActions(["getActivitesClient", "getActivityClient"]),
  },
  computed: {
    ...mapGetters(["gererAllActivites", "gererAllActivitesClient"]),
  },

  //   Load Page:
  created() {
    this.getActivitesClient();
    this.getActivityClient();
  },
};
</script>
<style scoped>
</style>
