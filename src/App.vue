<template>
  <div id="app">
    <h1 class="text-center my-5">Administrador de Citas Médicas</h1>
    <div class="container agendador">
      <form @submit.prevent="agregarCita" class="form-control p-4">
        <div class="row g-3">
          <div class="col">
            <label
              for="paciente"
              class="form-label"
              :style="{ color: form.Paciente ? 'black' : 'red' }"
              >Paciente</label
            >
            <input
              type="text"
              class="form-control"
              v-model="form.Paciente"
              @input="enabledForm"
              aria-label="paciente"
            />
          </div>
          <div class="col">
            <label
              for="fecha"
              class="form-label"
              :style="{ color: form.Fecha ? 'black' : 'red' }"
              >Fecha</label
            >
            <input
              type="date"
              class="form-control"
              v-model="form.Fecha"
              @input="enabledForm"
              aria-label="fecha"
            />
          </div>
          <div class="col">
            <label
              for="hora"
              class="form-label"
              :style="{ color: form.Hora ? 'black' : 'red' }"
              >Hora</label
            >
            <input
              type="time"
              class="form-control"
              v-model="form.Hora"
              @input="enabledForm"
              aria-label="hora"
            />
          </div>
          <div class="col">
            <label
              for="gravedad"
              class="form-label"
              :style="{ color: form.Gravedad ? 'black' : 'red' }"
              >Gravedad</label
            >
            <select
              name="gravedad"
              class="form-select"
              v-model="form.Gravedad"
              @input="enabledForm"
            >
              <option value="">Seleccionar</option>
              <option value="green">Baja</option>
              <option value="yellow">Media</option>
              <option value="red">Alta</option>
            </select>
          </div>
          <div class="col">
            <label
              for="motivo"
              class="form-label"
              :style="{ color: form.Motivo ? 'black' : 'red' }"
              >Motivo</label
            >
            <input
              type="text"
              class="form-control"
              v-model="form.Motivo"
              @input="enabledForm"
              aria-label="motivo"
            />
          </div>
        </div>
        <div class="row mt-3 d-grid col-4 mx-auto">
          <button class="btn btn-secondary" :disabled="!formValido">
            Agregar
          </button>
        </div>
      </form>
    </div>

    <div
      class="container consultas d-flex d-row justify-content-center align-items-center"
    >
      <div class="mt-5" v-if="citas.length === 0">
        <p class="text-center">Aún no hay consultas registradas</p>
      </div>
      <div class="mt-5 row" v-else>
        <CitaMedica
          v-for="(cita, index) in citas"
          :key="index"
          :paciente="cita.Paciente"
          :fecha="cita.Fecha"
          :hora="cita.Hora"
          :gravedad="cita.Gravedad"
          :motivo="cita.Motivo"
          @eliminar-cita="eliminarCita(index)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CitaMedica from "./components/CitaMedica.vue";

export default {
  name: "App",
  components: {
    CitaMedica,
  },
  data() {
    return {
      form: {
        Paciente: "",
        Fecha: "",
        Hora: "",
        Gravedad: "",
        Motivo: "",
      },
      formValido: false,
      citas: [],
    };
  },
  methods: {
    enabledForm() {
      if (
        this.form.Paciente &&
        this.form.Fecha &&
        this.form.Hora &&
        this.form.Gravedad &&
        this.form.Motivo
      ) {
        this.formValido = true;
      }
    },

    agregarCita() {
      this.citas.push({ ...this.form });

      this.form = {
        Paciente: "",
        Fecha: "",
        Hora: "",
        Gravedad: "",
        Motivo: "",
      };

      this.formValido = false;
    },

    eliminarCita(citaAEliminar) {
      this.citas.splice(citaAEliminar, 1);
    },
  },
};
</script>
