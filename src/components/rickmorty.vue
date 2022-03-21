<template>
  <div>
    <form>
      <label for="">Ingrese nombre Personaje</label>
      <br/>
      <input class="mt-5" type="text" v-model="busqueda" />
      <input type="submit" @click.prevent="fetchCharacter" value="Buscar" />
    </form>
    <section v-if='image !=""'>
      <img :src="image" alt="img" width="200px" class="ml-5" />
      <h4>Nombre: {{name}}</h4>
      <h4 class="mt-3">Habilidades</h4>
      <ul>
        <li v-for="habilidad in habilidades" :key="habilidad" >{{ habilidad }}</li>
      </ul>
      <h4>Movimientos</h4>
      <ul>
        <li v-for="movimiento in moves" :key="movimiento">{{ movimiento }}</li>
      </ul>
    </section>
    <section v-else>
        <h1>Buscar un personaje</h1>
    </section>
  </div>
</template>

<script>
export default {
  name: "pokemon-component",
  // props: {},
  data: function () {
    return {
      personaje: {
        name: "",
        sprite: "",
        abilities: [],
        moves: [],
      },
      busqueda:""
    };
  },
  computed: {
    image() {
      return this.personaje.sprite;
    },
    habilidades() {
      let new_array_habs = [];
      this.personaje.abilities.forEach((habilidad) => {
        new_array_habs.push(habilidad.ability.name);
      });
      return new_array_habs;
    },
    name() {
      return this.personaje.name;
    },
    moves() {
      let new_array_moves = [];
      this.personaje.moves.forEach((movimiento) => {
        new_array_moves.push(movimiento.move.name);
      });
      return new_array_moves;
    },
  },
  methods: {
    fetchCharacter() {
      // alert(this.personaje.name);
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.busqueda}`)
        .then((response) => response.json())
        .then((json) => {
          console.log(json);
          this.addCharacter(json);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    addCharacter(json) {
      let new_personaje = {
        name: json.name,
        sprite: json.sprites.front_default,
        abilities: json.abilities,
        moves: json.moves,
      };
      this.personaje = new_personaje;
    },
  },

  // -- Lifecycle Methods
  created() {
    this.fetchCharacter();
  },
  // -- End Lifecycle Methods
};
</script>

<style scoped>
input {
  margin-top: 10px;
}
li{
    list-style: none;
}
</style>