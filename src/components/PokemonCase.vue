<template>
  <div class="ContainerPokemon">
    <div class="iconPoke" v-bind:style="{'background-image': 'url(' + pokemon.sprites.other['official-artwork'].front_default + ')',}"></div>
    <span>{{pokemon.name}}</span>
  </div>
</template>

<script>
export default {
    name: "pokemonCase",
    props: {
        pokemon: {},
    },
};
</script>

<style scoped lang="scss">

.ContainerPokemon {
  width: 280px;
  padding: 13px 15px;
  border-radius: 15px;
  margin: 5% auto;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  cursor: pointer;
  background-color: white;
  align-items: center;
  display: flex;
  span{
      text-transform: capitalize;
  }
}
.ContainerPokemon:hover{
    background-color: #161616;
    font-weight: bold;
    color: white;
}
.ContainerPokemon:nth-child(2n) {
  margin-left: 25%;
}
.iconPoke {
  width: 44px;
  height: 44px;
  margin-right: 5%;
  border-radius: 50%;
  background-size: 70%;
  background-repeat: no-repeat;
  background-position: center;
  background-color: #363636;
}
</style>