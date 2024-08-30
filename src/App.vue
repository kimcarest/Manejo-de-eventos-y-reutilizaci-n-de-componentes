<template>
  <div id="app" class="mt-3">
    <main class="container p-3">
      <div class="text-center p-3">
        <h1>Consulta Médica</h1>
      </div>
      <form @submit.prevent="addConsulta">
        <div class="row">
          <div class="col-12 col-md-6 col-lg-2">
            <div class="text-center">
              <label for="paciente" v-if="nuevasConsulta.paciente" style="color: black">Paciente</label>
              <label for="paciente" v-else style="color: whitesmoke">Paciente</label><br />
              <input type="text" class="inputPaciente" name="paciente" required v-model="nuevasConsulta.paciente" />
            </div>
          </div>

          <div class="col-12 col-md-6 col-lg-2">
            <div class="text-center">
              <label for="fecha" v-if="nuevasConsulta.fecha" style="color: black">Fecha</label>
              <label for="fecha" v-else style="color: whitesmoke">Fecha</label><br />
              <input type="date" class="inputFecha" name="fecha" required v-model="nuevasConsulta.fecha" />
            </div>
          </div>

          <div class="col-12 col-md-6 col-lg-2 inputs">
            <div class="text-center">
              <label for="hora" v-if="nuevasConsulta.hora" style="color: black">Hora</label>
              <label for="hora" v-else style="color: whitesmoke">Hora</label><br />
              <input type="time" class="inputHora" name="hora" required v-model="nuevasConsulta.hora" />
            </div>
          </div>

          <div class="col-12 col-md-6 col-lg-2">
            <div class="text-center">
              <label for="gravedad" v-if="nuevasConsulta.gravedad" style="color: black">Gravedad</label>
              <label for="gravedad" v-else style="color: whitesmoke">Gravedad</label><br />
              <select name="gravedad" class="inputGravedad" v-model="nuevasConsulta.gravedad">
                <option disabled value="null" >Selecciona gravedad</option>
                <option v-for="(tipoGravedad, index) in tiposGravedad" :key="index" :value="tipoGravedad">
                  {{ tipoGravedad }}
                </option>
              </select>
            </div>
          </div>

          <div class="col-12 col-md-6 col-lg-2">
            <div class="text-center">
              <label for="motivo" v-if="nuevasConsulta.motivo" style="color: black">Motivo</label>
              <label for="motivo" v-else style="color: whitesmoke">Motivo</label><br />
              <textarea required class="inputMotivo" v-model="nuevasConsulta.motivo"></textarea>
            </div>
          </div>
          <div class="text-center">
            <button type="submit" class="btn btn-info" :disabled="!botonActivo">Agregar</button>
          </div>
        </div>
      </form>
    </main>
    <div class="text-center">
      <p v-show="consultas.length === 0" style="color: black">Aún no hay consultas registradas</p>
    </div>
    <hr>
    <section class="sectionCard p-5">
      <CardPaciente v-for="(consulta, index) in consultas" :key="index" :paciente="consulta.paciente"   
        :fecha="consulta.fecha" :hora="consulta.hora" :gravedad="consulta.gravedad" :motivo="consulta.motivo"
        @eliminarConsulta="eliminarConsulta(index)" />
    </section>

  </div>
</template>

<script>
import CardPaciente from "./components/CardPaciente.vue";      
export default {
  name: "App",  
  components: {   
    CardPaciente
  },
  data() {    
    return {
      tiposGravedad: ["baja", "media", "alta"],
      consultas: [],
      nuevasConsulta: {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: null,
        motivo: "",
      },
    };
  },
  methods: {    
    addConsulta: function () {
      this.consultas.push(this.nuevasConsulta);
      console.log(this.consultas);
      
      this.nuevasConsulta = {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
    },
    eliminarConsulta: function (index) {
      let consulta = this.consultas[index];
      if (confirm(`Esta seguro que desea eliminar la cita de ${consulta.paciente}?`)) {
        this.consultas.splice(index, 1);
      }
    }
  },
  computed: {   
    botonActivo: function () {
      return (
        this.nuevasConsulta.paciente &&
        this.nuevasConsulta.fecha &&
        this.nuevasConsulta.hora &&
        this.nuevasConsulta.gravedad &&
        this.nuevasConsulta.motivo
      );
    },
  },
};
</script>

<style>
main {
  border: 1px solid black;
  background-color: rgb(238, 138, 92); 
  border-radius: 10px;
  box-shadow: 5px 5px 5px 5px rgb(0, 0, 0, 0.3);
  margin: 20px;
  padding: 10px;
}
.row{
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
.inputPaciente{
  width: 165px;
}
.inputFecha{
  width: 165px;
}
.inputHora{
  width: 165px;
}
.inputGravedad{
  width: 165px;
}
.inputMotivo{
  width: 165px;
}

.sectionCard{
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap
}
.cardPaciente{
  width: 300px;
}
</style>