<template>
  <div>
    <v-card flat>
      <v-card-actions>
        <h1>Creación de Historias</h1>
        <v-spacer></v-spacer>
        <v-btn class="text-none" to="/historias">Ver lista de historias</v-btn>
      </v-card-actions>

      <v-form ref="formHistoria" v-model="valid" lazy-validation>
        <v-text-field
          v-model="historia.fecha"
          label="Fecha"
          :rules="rules.required"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.hora"
          label="Hora"
          :rules="rules.required"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.id"
          :rules="rules.required"
          label="Identificación"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.name"
          :rules="rules.required"
          label="Nombres"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.apellidos"
          :rules="rules.required"
          label="Apellidos"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.eps"
          :rules="rules.required"
          label="EPS"
          required
        ></v-text-field>

        <v-select
          v-model="historia.estadoCivil"
          :items="estadoCivil"
          label="Estado Civíl"
          item-value="id"  
          item-text="nombre"    
        ></v-select>
        
        <v-text-field
          v-model="historia.medicoTratante"
          :rules="rules.required"
          label="Médico Tratante"
          required
        ></v-text-field>

        <v-textarea
          v-model="historia.observaciones"
          :rules="rules.required"
          label="Observaciones"
          required
        ></v-textarea>
        <v-btn color="success" @click="saveHistoria()">Guardar historia</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    historia: {},
    idRules: [
      (v) => !!v || "El ID es obligatorio",
      (v) => /.+@.+\..+/.test(v) || "El ID no es valido",
    ],
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
    estadoCivil: [
      { id: 1, nombre: "Soltero" },
      { id: 2, nombre: "Casado" },
      { id: 3, nombre: "Unión Libre" },
      { id: 4, nombre: "Viudo" },
    ],
  }),
  beforeMount() {},

  methods: {
    /**
     * Enviar una solicitud (Request) en un método post
     * Para guardar el producto
     */
    async saveHistoria() {
      if (this.$refs.formHistoria.validate()) {
        console.log("-- Inicio guardar historia --");
        let historia = Object.assign({}, this.historia);
        let response = await this.$axios.post("http://localhost:3001/historias", historia);
        this.$swal.fire({
          type: "success",
          title: "Operación exitosa.",
          text: "El item se guardo correctamente.",
        });
      } else {
        this.$swal.fire({
          type: "warning",
          title: "Formulario incompleto.",
          text: "Hay campos que deben ser diligenciados.",
        });
      }
    },
  },
};
</script>

<style></style>
