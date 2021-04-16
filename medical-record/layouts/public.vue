<template>
  <v-app>
    <v-app-bar 
    fixed app
    dark
    color=#39F    
    >
    
      <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> -->
      <v-toolbar-title>Medical Record</v-toolbar-title>            
      
      <v-spacer></v-spacer>
    
      <v-btn icon @click.stop="dialogLogin = true" >               
        <v-icon
        large
        color=#FFFFFF  
        >
        mdi-account-key
        </v-icon>
      </v-btn>  
    </v-app-bar>

    <v-main>
      <nuxt />
    </v-main>
    <v-footer app color=#05c5d8>      
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

      <v-btn text to="/login" small class="text-none">
        <v-icon medium class="mr-2" color=#FFF> mdi-account-box </v-icon> 
        <h4>Médicos</h4>
        <style>
         h4 { color: #FFF; }
        </style>        
      </v-btn>      
    </v-footer>

    <!-- Login -->
    <v-dialog v-model="dialogLogin" max-width="290" persistent>
      <v-card>
        <v-card-text> </v-card-text>
        <login />
        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="green darken-1" text @click="dialogLogin = false">
            Cancelar
          </v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import login from "@/components/Login";
export default {
  beforeMount() {
    localStorage.clear();
  },
  components: {
    login,
  },
  data() {
    return {
      year: new Date().getFullYear(),
      dialogLogin: false,
    };
  },
};
</script>
<style></style>
