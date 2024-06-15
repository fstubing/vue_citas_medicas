<template>
  <div class="col">
    <div :style="{ backgroundColor: `${gravedad}` }" class="card">
      <div class="card-body">
        <p><strong>Paciente:</strong> {{ paciente }}</p>
        <p><strong>Fecha:</strong> {{ fecha }}</p>
        <p><strong>Hora:</strong> {{ hora }}</p>
        <p><strong>Motivo:</strong> {{ motivo }}</p>
        <button @click="$emit('eliminar-cita')" class="btn btn-secondary">
          Eliminar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["paciente", "fecha", "hora", "motivo", "gravedad"],
};
</script>

<style scoped>
.card {
  width: 18rem;
}
</style>
