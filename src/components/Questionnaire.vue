<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <div class="mb-3">
        <p>Quel lait a été utilisé pour fabriquer {{ fromage }} ?</p>
      </div>
      <div class="mb-3 mt-5 d-flex justify-content-around">
        <p @click="clickTypeLait('Vache')" v-bind:class="{'selected':typeLait==='Vache', 'notSelected': typeLait !== 'Vache'}">Vache</p>
        <p @click="clickTypeLait('Chèvre')" v-bind:class="{'selected':typeLait==='Chèvre', 'notSelected': typeLait !== 'Chèvre'}">Chèvre</p>
        <p @click="clickTypeLait('Brebie')" v-bind:class="{'selected':typeLait==='Brebie', 'notSelected': typeLait !== 'Brebie'}">Brebie</p>
      </div>
      <div class="text-end pe-5">
        <button type="submit" class="btn" style="background-color: #2EC4B6; color: #FFFFFF">Valider</button>
      </div>
    </form>
  </div>
  <div v-if="result === true" class="mt-lg-4 d-flex justify-content-center">
    <div class="alert alert-success text-center">
      Bonne réponse !
    </div>
  </div>
  <div v-else-if="result === false" class="mt-lg-4 d-flex justify-content-center">
    <div class="alert alert-warning text-center">
      Perdu, vous pouvez rejouer!
    </div>
  </div>
  <div v-else class="mt-lg-4 d-flex justify-content-center">
    <div class="alert alert-info text-center">
      Choisissez la bonne réponse.
    </div>
  </div>
</template>

<script>

export default {
  name: `Questionnaire`,
  props: [
    'objFromage',
      'scoreUser'
  ],
  data() {
    return {
      typeLaits: ["Vache", "Chèvre", "Brebie"],
      typeLait: '',
      typeLaitFrom: '',
      fromage: '',
      result: 'rien',
    }
  },
  watch: {
    objFromage() {
      if (this.objFromage !== null) {
        this.fromage = this.objFromage.fromage;
        this.typeLaitFrom = this.objFromage.lait;
      }
    },
  },
  methods: {
    clickTypeLait(e) {
      this.typeLait = e;
    },
    selected(e) {
      e.setStyle({
        border: "1px solid black",
      })
    },
    submitForm() {
      this.result = this.typeLaitFrom === this.typeLait;
      this.$emit('score', this.result)
    }
  }
}
</script>

<style scoped>
.selected {
  border: 3px solid #FF9F1C;
  background-color: #FFBF69;
  border-radius: 10px;
  padding: 5px;
  color: #FFFFFF;
  font-weight: bold;
}

.notSelected {
  border: 2px solid #2EC4B6;
  background-color: #FFFFFF;
  border-radius: 10px;
  padding: 5px;
  color: black;
}
</style>
