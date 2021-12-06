<template>
  <div style="height:100vh" >
    <div  :elevation="20" style="height:18%;background-color: #252525" >
    <!-- <img src="header2.jpg" style="height:100%;display:block;margin:auto" > -->
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXffSRsxD8GWe-wu5pDVEEaDAhEIdu1EBGfw&usqp=CAU" style="height:100%;display:block;margin:auto" >
    </div >
    
    <!-- <Login></Login> -->
    <router-view></router-view>
  </div>
</template>

<script>
//import NavBar from '@/views/Navbar'
//import Inicio from '@/views/Inicio'
//import Cronometro from '@/views/Cronometro'
//import BuscarAlumno from '@/views/BuscarAlumno'
//import VistaGeneral from '@/views/VistaGeneral'
// import Entrada from '@/components/Entrada'
// import Entrada from '@/components/Entrada'
// import VistaInterno from '@/views/VistaInterno'
// import Login from '@/views/Login'
export default {
  name: 'App',
  // components: { Login
   
  // },
  data () {
    return {
      navbar:true
    }
  },
   created(){
    this.vistaNavbar();
  },
  methods:{
    vistaNavbar(){
      if (this.$route.path == '/login') {
        this.navbar = false;
      }else{
        this.navbar = true;
      }
    }
  },
  beforeUpdate(){
    this.vistaNavbar();
    
  },
  updated(){
    this.vistaNavbar();
  }


  
}
</script>

<style>
.contenedor{
    padding: 0px;
    margin: 0;
    max-width: 100%;
  } 

  .container-main{
    margin-top: 60px;
  }
</style>


