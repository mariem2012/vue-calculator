<template>
  <div class="container mt-5">
    <h1>Calculatrice</h1>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="addition" value="addition" v-model="operation">
      <label class="form-check-label" for="addition">Addition</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="soustraction" value="soustraction" v-model="operation">
      <label class="form-check-label" for="soustraction">Soustraction</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="multiplication" value="multiplication" v-model="operation">
      <label class="form-check-label" for="multiplication">Multiplication</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="division" value="division" v-model="operation">
      <label class="form-check-label" for="division">Division</label>
    </div>

    <div v-if="operation">
      <div class="mt-3">
        <input type="number" class="form-control mb-2" v-model.number="valeur1" placeholder="Valeur 1">
        <input type="number" class="form-control mb-2" v-model.number="valeur2" placeholder="Valeur 2">
      </div>

      <button class="btn btn-primary mt-3" @click="calculer">Calculer</button>

      <div v-if="resultat !== null" class="mt-3">
        <h3>Résultat : {{ resultat }}</h3>
      </div>

      <div v-if="messageErreur" class="alert alert-danger mt-3">
        {{ messageErreur }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const operation = ref('')
const valeur1 = ref(null)
const valeur2 = ref(null)
const resultat = ref(null)
const messageErreur = ref('')

const calculer = () => {
  messageErreur.value = ''
  if (valeur1.value === null || valeur2.value === null) {
    messageErreur.value = 'Veuillez entrer deux valeurs.'
    return
  }
  switch (operation.value) {
    case 'addition':
      resultat.value = valeur1.value + valeur2.value
      break
    case 'soustraction':
      resultat.value = valeur1.value - valeur2.value
      break
    case 'multiplication':
      resultat.value = valeur1.value * valeur2.value
      break
    case 'division':
      if (valeur2.value === 0) {
        messageErreur.value = 'La division par zéro n\'est pas autorisée.'
        resultat.value = null
      } else {
        resultat.value = valeur1.value / valeur2.value
      }
      break
    default:
      messageErreur.value = 'Veuillez sélectionner une opération.'
      resultat.value = null
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
}
</style>
