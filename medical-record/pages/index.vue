<template>
  <div class="landing-page">
    <div class="VueMedicaLogo">        
      <!-- <h1>¡Bienvenido!</h1> -->     
      <img src="@/assets/logoInvert.png" height="250" width="250">
    </div>
  </div>  
     
</template>
<script>
export default {
  layout: "public",
  data: () => ({
    loading: false,
    selection: 1,
  }),
};
</script>

<style>
   .landing-page {
    background-image: url('../assets/backgDoctor.png');     
    height: 100vh;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;
  }
</style>

<style>
.VueMedicaLogo {  
  transform: rotateY(90deg);
  animation: turn 0.5s ease-out forwards 1s;     
}

@keyframes turn {
  100% {
    transform: rotateY(180deg);    
  }
}
</style>


