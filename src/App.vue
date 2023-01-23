<script setup>
import { ref, computed } from 'vue';

let name = "Vue dinamico";
let styleColor = "color: blue";
let arrayColores = ["blue", "red", "peru"];
let isActivo = false;
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
const arrayObjetosFrutas = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
  },
];

const fruta = {
  id: 1,
  name: "Naranja",
  price: "$3.00",
  description: "Una naranja"
};

const arrayObjetoFrutas2 = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
];

const activar = () => {
  console.log("se activo xD");
}

const mostrarAlerta = (mensaje) => console.log("mensaje: " + mensaje);

let counter = ref(0);
const operacion = (opc) => {
  if (opc == 0) {
    counter.value--;
  } else if (opc == 1) {
    counter.value++;
  } else {
    counter.value = 0;
  }
  verificaNumero();
}

let classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero"
  } else if (counter.value > 0) {
    return "positive"
  } else {
    return "negative";
  }
})

let arregloNumeros = ref([]);

let addNumero = () => {
  arregloNumeros.value.unshift(counter.value);
  verificaNumero();
}

let esHabilitado = ref(false);

let verificaNumero = () => {
  if (arregloNumeros.value.includes(counter.value)) {
    esHabilitado.value = true;
  } else {
    esHabilitado.value = false;
  }
}

let verificaColor = (numero) => {
  if (numero === 0) {
    return "zero"
  } else if (numero > 0) {
    return "positive"
  } else {
    return "negative";
  }
}
</script>

<template>

  <!--<h1>Hola {{ name.toUpperCase() }}</h1><br>-->
  <!--<h2 v-bind:style="styleColor">Soy azul</h2>-->
  <!--
  <h2 :style="styleColor">Soy azul</h2>
  <h2 :style="`color: ${arrayColores[2]}`">Soy Perú</h2>
  <h2>{{ isActivo? 'Estoy Activo': 'Estoy Desactivado' }}</h2>
  <h3 v-if="isActivo">Estoy Activo h3</h3>
  <h3 v-else>Estoy Inactivo h3</h3>
  -->
  <!-- <h3 v-if="!isActivo">Estoy Inactivo h3</h3> -->
  <!--
  <p v-show="true">Estoy Activo v-show</p>
  <p v-show="true">hola</p>
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index">
      {{ index }} - {{ fruta }}
    </li>
  </ul>
  <ul>
    <li v-for="(fruta, index) in arrayObjetosFrutas" :key="fruta.name">
      {{ index }} - {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
    </li>
  </ul>
  <ul>
    <li v-for="(value, propiedad, index) in fruta" :key="index">
      {{ index }} - {{ propiedad }} - {{ value }}
    </li>
  </ul>
  <ul>
    <template v-for="item in arrayObjetoFrutas2" :key="item.name">
      <li v-if="item.stock > 0">
        {{ item.name }} - {{ item.price }}
      </li>
    </template>
  </ul>
  -->

  <!--
  <button v-on:click="activar">Activame</button>
  <button v-on:click="mostrarAlerta('Texto 1')">Activame2</button>
  <button @click="activar">Activam3</button>
  -->
  <div class="container text-center mt-3">
    <div class="btn-group">
      <button @click="operacion(1)" class="btn btn-success">Incrementar</button>
      <button @click="operacion(0)" class="btn btn-danger">Decrementar</button>
      <button @click="operacion(2)" class="btn btn-secondary">Resetear</button>
      <button :disabled="esHabilitado" @click="addNumero()" class="btn btn-primary">Agregar</button>
    </div>
    <br>

    <!--<h2 :class="counter>0 ? 'positive' : 'negative'">{{ counter }}</h2>-->
    <h2 :class="classCounter">{{ counter }}</h2>

    <h3>Arreglo de Numeros: </h3>
    <ul class="list-group">
      <template v-for="numero in arregloNumeros">
        <li class="list-group-item mt-4">
          <span :class="verificaColor(numero)">{{ numero }}</span>
        </li>
      </template>
    </ul>
  </div>
</template>
<style>
.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}

h1 {
  color: red;
  font-size: 50px;
}
</style>

<!--
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
-->