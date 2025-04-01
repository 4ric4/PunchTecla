<template>
  <div id="app">
    <h1>Jogo de Placas</h1>
    <p>Pontos: {{ points }}</p>
    <p>Placa: {{ currentPlate }}</p>
    <p>Pressione a tecla correta!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      points: 0, // Pontos do jogador
      currentPlate: "", // Tecla da placa que está sendo exibida
      validKeys: ["a", "b", "c", "d", "e"], // Teclas válidas
    };
  },
  mounted() {
    this.generatePlate(); // Gera a primeira placa quando o componente é montado
    window.addEventListener("keydown", this.handleKeyPress); // Captura pressionamento de tecla
  },
  unmounted() {
    window.removeEventListener("keydown", this.handleKeyPress); // Remove o listener quando o componente é desmontado
  },
  methods: {
    // Função que gera uma nova placa (tecla aleatória)
    generatePlate() {
      const randomKey = this.validKeys[Math.floor(Math.random() * this.validKeys.length)];
      this.currentPlate = randomKey;
      console.log(`Placa gerada: ${this.currentPlate}`); // Log para verificar qual placa foi gerada
    },

    // Função que lida com a tecla pressionada
    handleKeyPress(event) {
      console.log(`Tecla pressionada: ${event.key}`); // Log para verificar a tecla pressionada
      if (event.key === this.currentPlate) {
        this.points += 10; // Ganha pontos por acerto
        this.generatePlate(); // Gera uma nova placa
      } else {
        this.points = Math.max(0, this.points - 5); // Perde pontos por erro
      }
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 20px;
  color: #2c3e50;
}

p {
  font-size: 24px;
  margin: 10px 0;
}

h1 {
  font-size: 32px;
  color: #42b983;
}
</style>
