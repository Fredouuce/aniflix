<template>
  <main class="main_container">
    <!-- Formulaire de recherche -->
    <div class="welcome">
      <h1>
        Bienvenue sur
        <span class="aniflix">Aniflix</span>
      </h1>
      <div>
        <label for="search_anime"
          >Veuillez chercher un anime qui vous plais</label
        >
        <br />
        <input
          name="search_anime"
          id="search_anime"
          type="text"
          v-model="searchInput"
          placeholder="Rechercher"
          @input="searchAnime"
        />
      </div>

      <h2>{{ searchInput }}</h2>
    </div>
    <!-- Affichages des mangas -->
    <h1 v-if="isLoading">ça charge</h1>
    <div>
      <div v-if="isLoading == false && searchedAnime.length <= 0">
        <!-- Top mangas -->
        <h1>Notre séléction :</h1>
        <div class="main_card_container">
          <div v-for="search in animes" :key="search.id">
            <Card :anime="search" />
          </div>
        </div>
      </div>
      <div v-if="searchedAnime.length > 0">
        <!-- Manga rechercher -->
        <h1>Votre recherche : {{ searchInput }}</h1>
        <div class="main_card_container">
          <div v-for="anime in searchedAnime" :key="anime">
            <Card :anime="anime" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import Card from "../components/Card";
export default {
  name: "Home",
  components: {
    Card,
  },
  data() {
    return {
      searchInput: "",
      animes: [],
      isLoading: true,
      searchedAnime: [],
    };
  },
  methods: {
    searchAnime() {
      this.isLoading = true;
      axios
        .get(`https://kitsu.io/api/edge/anime?filter[text]=${this.searchInput}`)
        .then((response) => {
          this.searchedAnime = response.data.data;
          this.isLoading = false;
          console.log(this.searchedAnime);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    axios
      .get(`https://kitsu.io/api/edge/trending/anime`)
      .then((response) => {
        this.animes = response.data.data;
        this.isLoading = false;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
.welcome {
  text-align: center;
}
#search_anime {
  margin-top: 1em;
  width: 300px;
  height: 40px;
  border: none;
  border-radius: 5px;
  padding-left: 20px;
}
.main_card_container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.main_container {
  padding: 1em;
  max-width: 1400px;
  position: relative;
  left: 50%;

  transform: translateX(-50%);
  background: #292929;
}

.aniflix {
  color: #e50914;
  letter-spacing: 2px;
}
</style>
