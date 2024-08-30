<template>
    <div class="p-3 row">  
      <div class="cardPaciente col-12 col-md-4 col-lg-4 p-3" :style="colorCard()"> 
        <div class="cardTitle text-center"> 
          <h3>Paciente</h3>
          <p>{{ paciente }}</p>
        </div>
        <div class="cardBody text-center"> 
          <h3>Fecha</h3>
          {{ fecha }}
          <h3>Hora</h3>
          {{ hora }}
          <h3>Motivo</h3>
          {{ motivo }}
        </div>
        <div class="cardFooter text-center p-2 mt-3">  
          <button class="btn btn-info" @click="$emit('eliminarConsulta')">
            Eliminar
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "CardPaciente",   
    props: {
      paciente: String,
      fecha: String,
      hora: String,
      gravedad: String,
      motivo: String,
    },
    methods: {    
      colorCard: function () {  
        if (this.gravedad === "baja") {
          return { backgroundColor: "green", color: "black" };
        } else if (this.gravedad === "media") {
          return { backgroundColor: "yellow", color: "black" };
        } else if (this.gravedad === "alta") {
          return { backgroundColor: "red", color: "white" };
        }
        console.log(this.gravedad); 
      },
    },
  };
  </script>
  
  <style scoped>  
  .cardPaciente{
      width: 300px;
      margin: 10px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    }
  
  </style>