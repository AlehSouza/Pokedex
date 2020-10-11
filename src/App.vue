<template>
  <div id="app">
    <div id="container">
      <div id="searchPoke">
        <input
          type="text"
          placeholder="Procure seu pokemon favorito"
          id="searchPokeInput"
        />
        <button v-on:click="searchPoke()"></button>
      </div>
      <div id="pokeSprite"></div>
      <div id="buttonsCase">
        <button v-on:click="prevPoke(pokeId)"></button>
        <button v-on:click="nextPoke(pokeId)"></button>
      </div>
      <div class="left">
        <div class="listPokemons">
          <div
            v-for="(poke, x) in pokemons"
            :key="x"
            v-on:click="setOnPokedex(x)"
          >
            <PokemonCase :pokemon="poke" />
          </div>
        </div>
      </div>
      <div class="right">
        <h1>Pokedéx</h1>
        <h2 id="namePoke">Aproveite :)</h2>
        <div class="InfoPoke">
          <div class="boxInfo">
            <span>ID</span>
            <span id="idPoke"></span>
          </div>
          <div class="boxInfo">
            <span>Height</span>
            <span id="HeightPoke"></span>
          </div>
          <div class="boxInfo">
            <span>Weight</span>
            <span id="WeightPoke"></span>
          </div>
          <div class="boxInfo">
            <span>Type</span>
            <span id="TypePoke"></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PokemonCase from "./components/PokemonCase";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      pokeId: 0,
      pokeSearchName: "",
      pokeSearchArray: [],
    };
  },
  components: {
    PokemonCase,
  },
  created: function () {
    for (let i = 0; i <= 150; i++) {
      axios.get("https://pokeapi.co/api/v2/pokemon/" + i).then((resp) => {
        this.pokemons.push(resp.data);
      });
    }
  },
  methods: {
    setOnPokedex(x) {
      this.pokeId = x;
      document.getElementById("pokeSprite").style.backgroundImage =
        "url(" +
        this.pokemons[x].sprites.other["official-artwork"].front_default +
        ")";
      document.getElementById("namePoke").innerHTML = this.pokemons[x].name;
      document.getElementById("idPoke").innerHTML = this.pokemons[x].id;
      document.getElementById("HeightPoke").innerHTML = this.pokemons[x].height;
      document.getElementById("WeightPoke").innerHTML = this.pokemons[x].weight;
      document.getElementById("TypePoke").innerHTML = this.pokemons[
        x
      ].types[0].type.name;
    },
    nextPoke(pokeId) {
      this.pokeId++;
      if (pokeId <= 150) {
        document.getElementById("pokeSprite").style.backgroundImage =
          "url(" +
          this.pokemons[pokeId].sprites.other["official-artwork"]
            .front_default +
          ")";
        document.getElementById("namePoke").innerHTML = this.pokemons[
          pokeId
        ].name;
        document.getElementById("idPoke").innerHTML = this.pokemons[pokeId].id;
        document.getElementById("HeightPoke").innerHTML = this.pokemons[
          pokeId
        ].height;
        document.getElementById("WeightPoke").innerHTML = this.pokemons[
          pokeId
        ].weight;
        document.getElementById("TypePoke").innerHTML = this.pokemons[
          pokeId
        ].types[0].type.name;
      }
      console.log(this.pokeId);
    },
    prevPoke(pokeId) {
      this.pokeId--;
      if (pokeId <= 150) {
        document.getElementById("pokeSprite").style.backgroundImage =
          "url(" +
          this.pokemons[pokeId].sprites.other["official-artwork"]
            .front_default +
          ")";
        document.getElementById("namePoke").innerHTML = this.pokemons[
          pokeId
        ].name;
        document.getElementById("idPoke").innerHTML = this.pokemons[pokeId].id;
        document.getElementById("HeightPoke").innerHTML = this.pokemons[
          pokeId
        ].height;
        document.getElementById("WeightPoke").innerHTML = this.pokemons[
          pokeId
        ].weight;
        document.getElementById("TypePoke").innerHTML = this.pokemons[
          pokeId
        ].types[0].type.name;
      }
    },
    searchPoke() {
      this.pokeSearchName = document
        .getElementById("searchPokeInput")
        .value.toLowerCase();
      axios
        .get("https://pokeapi.co/api/v2/pokemon/" + this.pokeSearchName)
        .then((respSearch) => {
          console.log(respSearch.data.name);
          this.pokeId = respSearch.data.id;
          document.getElementById("pokeSprite").style.backgroundImage =
            "url(" +
            respSearch.data.sprites.other["official-artwork"].front_default +
            ")";
          document.getElementById("namePoke").innerHTML = respSearch.data.name;
          document.getElementById("idPoke").innerHTML = respSearch.data.id;
          document.getElementById("HeightPoke").innerHTML =
            respSearch.data.height;
          document.getElementById("WeightPoke").innerHTML =
            respSearch.data.weight;
          document.getElementById("TypePoke").innerHTML =
            respSearch.data.types[0].type.name;
        });
    },
  },
};
</script>

<style scoped lang="scss">
body,
html {
  overflow-y: hidden !important;
}
@import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: #f1f1f125;
}

::-webkit-scrollbar-thumb {
  background: rgba(32, 32, 32, 0.527);
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

* {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  font-family: "Raleway", sans-serif;
  outline: none !important;
}

#container {
  width: 100%;
  height: 100vh;
  display: flex;
}

#pokeSprite {
  width: 500px;
  height: 500px;
  margin-top: 20vh;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  background-color: white;
  background-size: 80%;
  background-repeat: no-repeat;
  background-position: center;
  background-image: url("../src/assets/pokeballjpeg.png");
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  border-radius: 50%;
  position: absolute;
  transition: 1s;
}

#searchPoke {
  width: 300px;
  height: 50px;
  border-radius: 15px;
  background-color: white;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  margin-top: 2vh;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  position: absolute;
  overflow: hidden;
  justify-content: center;
  align-items: center;
  display: flex;
  z-index: 1;
  animation: softMoveInput 5s;
  input {
    width: 70%;
    padding: 12px;
    border: 0px;
    background-color: transparent;
  }
  button {
    width: 38px;
    height: 38px;
    cursor: pointer;
    background-image: url("./assets/searchicon.png");
    background-size: 60%;
    background-position: center;
    background-repeat: no-repeat;
    background-color: #f23e3e;
    border: 0px;
    border-radius: 50px;
    justify-content: center;
    align-items: center;
    display: flex;
  }
}

@keyframes softMoveInput {
  to {
    margin-top: 2vh;
  }
  80% {
    margin-top: -8vh;
  }
  from {
    margin-top: -8vh;
  }
}

#buttonsCase {
  width: 400px;
  height: 60px;
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  bottom: 50px;
  animation: softMoveButtons 5s;
  justify-content: space-between;
  display: flex;
  button {
    width: 60px;
    height: 60px;
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
    border-radius: 50px;
    border: 0px;
    cursor: pointer;
    background-image: url("./assets/arrow.png");
    background-position: 18px center;
    background-repeat: no-repeat;
    background-size: 50%;
  }
  button:nth-child(1) {
    transform: rotate(180deg);
  }
}

@keyframes softMoveButtons {
  to {
    bottom: 50px;
  }
  80% {
    bottom: -150px;
  }
  from {
    bottom: -150px;
  }
}

#namePoke {
  text-transform: capitalize;
}

.left {
  width: 50%;
  height: 100%;
  background-color: #f23e3e;
}

.right {
  width: 50%;
  height: 100%;
  background-color: #363636;
  background-image: url("./assets/pokeballpng.png");
  background-repeat: no-repeat;
  background-size: 60%;
  background-position: 150% 150%;
  h1 {
    text-align: right;
    padding: 40px 50px;
    margin: 0px;
    font-size: 170px;
    opacity: 0.3;
  }
  h2 {
    text-align: center;
    font-size: 45px;
    color: white;
  }
}

.InfoPoke {
  width: 400px;
  justify-content: space-between;
  flex-wrap: wrap;
  display: flex;
  margin: 20px 40%;
  span {
    text-transform: capitalize;
  }
}

.boxInfo {
  width: 40%;
  height: 20px;
  margin: 2%;
  padding: 12px;
  border-radius: 5px;
  background-color: white;
  justify-content: space-between;
  display: flex;
  span {
    font-weight: bold;
    transition: 1s;
  }
}

.listPokemons {
  width: 500px;
  height: 90%;
  margin: 4%;
  overflow: auto;
  padding: auto;
}
</style>
