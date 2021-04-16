<template>
  <div>
    <v-card flat>
      <v-card-actions>
        <h1>Edición de Historias</h1>
        <v-spacer></v-spacer>
        <v-btn class="text-none" to="/historias">Ver Historias</v-btn>
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
          label="Identificación"
          :rules="rules.required"
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

        <v-text-field
          v-model="historia.estadoCivil"
          :rules="rules.required"
          label="Estado Civíl"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.medicoTratante"
          :rules="rules.required"
          label="Médico Tratante"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.observaciones"
          :rules="rules.required"
          label="Observaciones"
          required
        ></v-text-field>        
        <v-btn color="success" @click="updateHistoria()">Modificar Historia</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  async asyncData({ params }) {
    let id_historia = params.id;
    return { id_historia };
  },

  data: () => ({
    valid: true,
    historia: {},    
    idRules: [
      (v) => !!v || "La identificación es obligatoria",
      (v) => /.+@.+\..+/.test(v) || "La identificación no es válido",
    ],
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
  }),
  beforeMount() {
    this.getHistoria();
  },

  methods: {
    /**
     * Enviar una solicitud (Request) en un método get
     * Para obtener una sola historia dado el código
     */
    async getHistoria() {
      try {
        //
        let response = await this.$axios.get(
          "http://localhost:3001/historias/" + this.id_historia
        );
        this.historia = response.data;
      } catch (error) {
        this.$swal
          .fire({
            type: "error",
            title: "Oops...",
            text: "La historia no existe o hubo un error cargandola.",
            allowEscapeKey: false,
            allowOutsideClick: false,
          })
          .then((result) => {
            if (result.value) {
              this.$router.push("/historias");
            }
          });
      }
    },

    /**
     * Enviar una solicitud (Request) en un método update
     * Para modificar la historia
     */
    async updateHistoria() {
      if (this.$refs.formHistoria.validate()) {
        // Crear un nuevo objeto con la info de la historia
        let historia = Object.assign({}, this.historia);
        let response = await this.$axios.put(
          "http://localhost:3001/historias/" + this.id_historia,
          historia
        );
        this.$swal.fire({
          type: "success",
          title: "Operación exitosa.",
          text: "El item se actualizó correctamente.",
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
