<script>
export default {
  name: 'StyleForm',
  data() {
    return {
      backgroundColor: '',
      color: '',
      borderRadius: '',
      opcionesFont: ['normal', 'cursive', 'monospace', 'sans-serif'],
      tipoFont: '',
      mostrartexto: false,
      texto: '',
      opaco: false,
      opcionesTamaño: ['Pequeño', 'Mediano', 'Grande'],
      tamañoLetra: ''
    }
  }
}
</script>

<template>
  <div class="container">
    <form>
      <div class="flex-group">
        <label>Color de Fondo</label>
        <input type="color" v-model="backgroundColor" />
      </div>

      <div class="flex-group">
        <label>Color de Texto</label>
        <input type="color" v-model="color" />
      </div>

      <div class="check-group">
        <label>Mostrar Texto</label>
        <input type="checkbox" v-model="mostrartexto" />
      </div>

      <div class="flex-group">
        <label>Borde</label>
        <input type="range" min="0" max="50" v-model="borderRadius" />
      </div>

      <div class="flex-group">
        <label>Contenido textual</label>
        <textarea v-model="texto"></textarea>
      </div>

      <div class="flex-group">
        <label>Tipografía</label>
        <select v-model="tipoFont">
          <option v-for="(font, index) in opcionesFont" :key="index" :value="font">
            {{ font }}
          </option>
        </select>
      </div>

      <div class="check-group">
        <label>Opaco</label>
        <input type="checkbox" v-model="opaco" />
      </div>

      <div class="flex-group">
        <label>Tamaño de Letra</label>
        <ul>
          <li v-for="opcion in opcionesTamaño" :key="opcion">
            <input type="radio" name="opcionesTamaño" :value="opcion" v-model="tamañoLetra" />
            {{ opcion }}
          </li>
        </ul>
      </div>
    </form>

    <section v-show="backgroundColor || (color && mostrartexto)">
      <div
        class="box"
        :style="{
          backgroundColor: backgroundColor,
          color: color,
          borderRadius: borderRadius + '%',
          fontFamily: tipoFont,
          fontSize: tamañoLetra === 'Pequeño' ? '14px' : tamañoLetra === 'Mediano' ? '20px' : '36px'
        }"
        :class="{ opaco: opaco }"
      >
        <p v-show="mostrartexto">{{ texto }}</p>
      </div>
    </section>
  </div>
</template>

<style scoped>
.container {
  min-height: 80vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 3rem;
  place-content: center;
}

form {
  background-color: rgba(14, 58, 61, 0.877);
  padding: 1.5rem;
  color: lightgray;
}

label {
  margin: 0.5rem 0;
}

.flex-group {
  display: flex;
  flex-direction: column;
}

.check-group {
  margin: 0.8rem 0;
}

.check-group label {
  margin-right: 0.5rem;
}

ul {
  list-style-type: none;
  display: flex;
  column-gap: 1rem;
}

section {
  margin: auto;
}

.box {
  width: 300px;
  height: 300px;
  display: grid;
  place-content: center;
}

.opaco {
  opacity: 0.5;
}
</style>
