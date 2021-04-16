<template>  
  <v-app>
    <!-- Menú hamburguesa -->
    <v-navigation-drawer v-model="openMenu" fixed app color=#1e73be >
      <v-list>
        <v-list-item v-for="item in items" :key="item.id" :to="item.to" router exact>
          <v-list-item-action>
            <v-icon style="color:#FFFFFF">{{ item.icon }}</v-icon>
          </v-list-item-action>

          <v-list-item-content style="color:#FFFFFF">
            <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Barra de navegación superior -->
    <v-app-bar fixed app color=#39F>

      <!-- Icono que controla el menú hamburguesa -->
      <v-app-bar-nav-icon color="white" @click.stop="openMenu = !openMenu" />
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>

    <v-footer app color=#222> 
    <v-spacer></v-spacer>      
     <div>
        <center>
          <span>&copy; {{ year }}</span>
          <br />
          <small>Medical Record</small>
          <style>
            small { color: #FFF; }
            span { color: #FFF; }
          </style>
        </center>
      </div>
      <v-spacer></v-spacer>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  beforeMount() {
    this.loadUser();
  },
  data() {
    return {
      year: new Date().getFullYear(),
      openMenu: false,
      items: [
        {
          id: "",
          icon: "",
          title: "",          
        },
        {
          id: "home",
          icon: "mdi-home",
          title: "Inicio",
          to: "/",
        },
        {
          id: "historias",
          icon: "mdi-file-document",
          title: "Historias",         
          to: "/historias",

        },
        {
          icon: "mdi-account-multiple",
          title: "Usuarios",
          to: "/users",
        },
        {
          icon: "mdi-exit-to-app",          
          title: "Cerrar sesión",
          to: "/",
        },
      ],
    };
  },
  methods: {
    loadUser() {
      let stringUser = localStorage.getItem("user-in");
      this.user = JSON.parse(stringUser);
      this.validRol(this.user);
    },
    validRol(user) {
      if (!user || (user.rol != 1 && user.rol != 2)) {
        this.$router.push("/");
      }
    },
  },
};
</script>
