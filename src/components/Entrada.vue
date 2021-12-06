<template>
        <!-- <v-container grid-list-md text-xs-center> -->
        <div class="wrapper wrapper-login cont">
        <div  class="left-layout">
            <div  style="background-image: url(Izquierdo.JPG);" class="left-layout-before"></div>
            
        </div>
       
        <div v-bind:style="{'background-image': 'linear-gradient(rgba(255, 255, 255, 0.75),rgba(255, 255, 255, 0.75)),url(' + this.right_bg + ')'}" class="right-layout">
            <!-- <v-layout style="align-items:center;height:100%"> -->
                <div class="wrap-right">
            <!-- <v-flex     xs4 > -->
                <div  style="font-size: 2rem !important;text-align:center;margin-left: 24%;margin-bottom: 147px;">
                     <v-text style="color:#252525">RELOJ</v-text>
                    <div class="reloj">
                         <p id="reloj" style="margin-top: -16px;"></p>
                        </div>
                    <!-- <div>
                    &nbsp;&nbsp;{{this.horas}}:{{this.minutos}}:{{this.segundos}}
                    </div>   -->
                    <v-card-text style="color:#FFF;margin-bottom: 31px;position:relative;z-index:1" >
                            REGISTRE SU INGRESO
                        <div class="bg-title-after"></div>
                    </v-card-text>
                    <!-- <span style="color:#FFF">Registro de Visitantes </span> -->
                <!-- <v-card-text>
                Ingresa su código de matricula
                </v-card-text> -->
                <v-card-text>
                <v-text-field  autofocus    name="Codigo" label="Ingrese su DNI  aqui..."  class="validar"  v-model="Codigo" ></v-text-field>
                </v-card-text>
                <v-row justify="center">
                    <v-dialog 
      v-model="dialogEntrada"
      persistent
      max-width="800"
      
      
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          v-on:click.prevent="Filtro"
        >
          Marcar Ingreso
        </v-btn>
      </template>
                    <v-card style="padding:30px;"  >
                        <v-card-title class="headline" style="background: #222831;padding: 20px;color: #FFF;">
                        Tenga un buen dia!
                        </v-card-title>
                        <v-card-text style="padding: 15px;">
                                  <v-form  @submit.prevent="submit">
                                                                                   
                                        <v-layout row>

                                         <v-flex xs6 style="padding: 0 35px;">
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Nombres"
                                            :error-messages="errors"
                                            label="Nombre"
                                            required
                                            ></v-text-field>
                                      
                                            <!-- <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Condicion_Laboral"
                                            :error-messages="errors"
                                            label="Condicion Laboral"
                                            required
                                            ></v-text-field>
                                    
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Edad"
                                            :error-messages="errors"
                                            label="Edad"
                                            required
                                            ></v-text-field>

                                            <v-text-field :readonly="shouldDisable"
                                            v-model="this.Correo"
                                            :error-messages="errors"
                                            label="Correo"
                                            required
                                            ></v-text-field>
                                    
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Fecha_Nacimiento"
                                            :error-messages="errors"
                                            label="Fecha Nacimiento"
                                            required
                                            ></v-text-field> -->
                                            </v-flex>
                                        <v-flex xs6 style="padding: 0 35px;">
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.codigo"
                                            :error-messages="errors"
                                            label="DNI"
                                            required
                                            ></v-text-field>
                                      
                                            <!-- <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Modalidad_Contrato"
                                            :error-messages="errors"
                                            label="Modalidad"
                                            required
                                            ></v-text-field>
                                    
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="alumno.Sexo"
                                            :error-messages="errors"
                                            label="Sexo"
                                            required
                                            ></v-text-field>

                                            <v-text-field :readonly="shouldDisable"
                                            v-model="this.Celular"
                                            :error-messages="errors"
                                            label="Celular"
                                            required
                                            ></v-text-field> -->
                                    
                                            <v-text-field :readonly="shouldDisable"
                                            v-model="Registra"
                                            :error-messages="errors"
                                            label="Registrado"
                                            required
                                            ></v-text-field>
                                            </v-flex>  

                                        </v-layout>
                                         
                                        </v-form>
                        </v-card-text>
                        <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn
                            style="background-color:#1dd8d8;color:#FFFF"
                            text
                            @click="dialogEntrada = false"
                        >
                            Exit
                        </v-btn>
                        </v-card-actions>
                    </v-card>
        </v-dialog>

    <v-dialog 
      v-model="dialogSalida"
      persistent
      max-width="800"
      
      
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          v-on:click.prevent="FiltroSalida"
        >
          Marcar Salida
        </v-btn>
      </template>  
      <v-card style="padding:30px;"  >
                        <v-card-title class="headline" style="background: #222831;padding: 20px;color: #FFF;">
                        Tenga un buen dia!
                        </v-card-title>
                        <v-card-text style="padding: 15px;">
                                  <v-form  @submit.prevent="submit">
                                                                                   
                                        <v-layout row>

                                         <v-text-field :readonly="shouldDisable"
                                            v-model="MensajeSalida"
                                            :error-messages="errors"
                                            label="Salida"
                                            required
                                            ></v-text-field>

                                        </v-layout>
                                         
                                        </v-form>
                        </v-card-text>
                        <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn
                            style="background-color:#1dd8d8;color:#FFFF"
                            text
                            @click="salir"
                        >
                            Exit
                        </v-btn>
                        </v-card-actions>
                    </v-card>
     </v-dialog>

     
  </v-row>
                <!-- <v-card-text>
                    <v-layout>
                    <v-flex>
                         <v-layout text-center>
                            <v-btn style="margin:auto;background-color:#252525;color:white;padding: 0 40px;font-size: 1.6rem !important;-webkit-box-shadow: 6px 7px 5px -2px rgba(0,0,0,0.32);
                            -moz-box-shadow: 6px 7px 5px -2px rgba(0,0,0,0.32);
                            box-shadow: 6px 7px 5px -2px rgba(0,0,0,0.32)" v-on:click.prevent="Filtro"  v-on="on" >Aceptar</v-btn>
                        </v-layout>
                    </v-flex>
                    </v-layout>
                </v-card-text> -->
                </div>
               <!-- <button color="primary"
          dark onclick="location.href='/#/Tablas'" >admi Temporal</button> -->
            </div>
            
             
             <!-- </v-layout> -->
        </div>
                     
        </div>
 
    <!-- </v-container> -->
    <!-- @keydown.enter="Filtro" -->
</template>

<script>

import axios from 'axios';

export default {
        components:{ 
               

        },

    data(){
        return{
            cont :0,
            Indice:0,
            i:0,
            MensajeSalida:'Gracias por Marcar su Salida',
            segundos: '00',
            minutos: '00',
            horas: '00',
            horaRecibida: '',
            shouldDisable:true,
            Correo:'',
            Celular:'',
            Registra:"Registro con exito",
            Nombres:'',
            Espacio:"/",
            name:"Marco",
            dialogEntrada: false,
            dialogSalida: false,
            Codig:'',
            Codigo:'',
            Interno:0,
            Externo:0,
            maximo:0,
            estado:false,
            busqueda:false,
            alumno: [],
            e:[],
            Recuperando: [],
            RegistradosHoy: [],
            alumnoSalida: [],
            right_bg:'Derecho.JPG'

        }
    },
    methods: {
        RegistrarUsuarioInterno(Codig){
                if(this.Interno==1){ 
                   // // this.Codig= this.Codigo.substr(2,9);
                    console.log('hans gay Interno');
                    this.GuardarUsuarioInterno(this.Codig);
                    // this.$router.push('https://asistenciacc.000webhostapp.com/')
                    // this.$router.push({
                    //                 name: "vistaInterno",
                    //                 params:{
                    //                     codigo: this.Codig,
                    //                 }
                    //                 });
                   
                    
                }

                else{   if(this.Externo==1){
                        console.log('hans gay Externo');
                        this.GuardarUsuarioExterno(this.Codig);
                        // this.$router.push('https://asistenciacc.000webhostapp.com/')
                            // this.$router.push({
                            //         name: "vistaExterno",
                            //         params:{
                            //             codigo: this.Codig,
                            //         }
                            //         });
                            
                            }
                        else{
                           
                        }
                }


        },
        GuardarUsuarioInterno(){
            console.log("entrando al metodo de guardado");
            console.log(this.Codig+'Metodo GuardarUsuariointerno');
            axios.post('http://192.168.2.71/apiregistro/v1/internos/'+this.Codig,
                {   
            //  id:this.Codigo,
            
                 },
                {headers:{
             'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8' }}
                 ).then((response)=>{
                this.Codigo='';
                
              

         }

         )
        },
        FiltroSalida(){
            console.log("Esta en el metodo FILROSALIDA");
          if(this.Codigo.length==8){
                    if(this.Codigo.startsWith("0")){
                        console.log(this.Codigo);
                        if(this.Codigo.startsWith("00")){
                           
                           if(this.Codigo.startsWith("000")){
                               this.Codig=this.Codigo.substring(3,8);
                                console.log(this.Codigo +" codigo quitando 000");
                                this.ExtrayendoId(); 
                           }
                           else{
                                this.Codig=this.Codigo.substring(2,8);
                                console.log(this.Codigo +" codigo quitando 00");
                                this.ExtrayendoId(); 
                           }
                        }
                        else{
                            this.Codig=this.Codigo.substring(1,8);
                            console.log(this.Codigo +" codigo quitando 0");
                            this.ExtrayendoId();

                        }    

                        }   
                    else{
                    this.Codig=this.Codigo;//Codigo de visitante
                    console.log(this.Codigo);
                    this.ExtrayendoId();}
                }
                if(this.Codigo.length==7){
                this.Codig=this.Codigo;//Codigo de Graduado y Docente
                
                this.ExtrayendoId();
                }      

        },
        ExtrayendoId(){
                console.log("Estas en el metodo Extrayendo ID");
                axios.get("/apiregistro/v1/internos",
                    {headers: { 'content-type': 'application/form-data'  }})
                    
                    .then((response)=>{
                        console.log("Metodo extrayendo a continuacion codigo");
                        console.log(this.Codigo);
                        this.Recuperando = response.data;
                        console.log("Recuperando datos de Recuperando");
                        console.log(this.Recuperando)
                        this.Recuperando.forEach(Recuperando=>{
                                         console.log("ESTAS EN EL METODO MAXIMO ID");
                                        console.log(this.Codigo);
                                        console.log(Recuperando.IntCod);
                                        // this.Id_Maximo(Recuperando);
                                        if(Recuperando.IntCod  == this.Codig){
                                            console.log(Recuperando);
                                        this.RegistradosHoy.push(Recuperando);
                                        this.cont= this.cont+1;
                                        console.log(this.cont);
                                        console.log("Aqui vienen las cadena nueva");
                                        console.log(this.RegistradosHoy);
                                }

                        
                                    })
                
                        console.log("Aqui vamos");
                        console.log(this.RegistradosHoy);
                        // console.log(this.RegistradosHoy[1].IntCod);
                        this.maximo = this.RegistradosHoy[0].Indice; // Declaramos e inicializamos el máximo.
                         console.log(this.maximo+" es el numero maximo");
                         console.log(this.cont);
                         this.Indice=this.RegistradosHoy[this.cont-1].Indice;
                         console.log(this.Indice);
                        this.Salida();
                        // for ( this.i = 0; this.i <= 2; i++){
                        //     console.log("Rickolas!!!");
                        // // if (this.maximo < this.RegistradosHoy[i].Indice){
                        // //     this.maximo = this.RegistradosHoy[i].Indice;}
                        //     } 
                        // this.Indice = this.maximo;
                        // console.log("Aqui viene el Indice");
                        // console.log(this.Indice);
                        // this.Salida();
                        
                    })
                    .catch(e=>{
                        this.errors.push(e);
                    });
                        // for ( this.i = 0; this.i <= 2; i++){
                        //     console.log("Rickolas!!!");
                        // if (this.maximo < this.RegistradosHoy[i].Indice){
                        //     this.maximo = this.RegistradosHoy[i].Indice;}
                            // } 
                    //  maximo = this.RegistradosHoy.Indice[0]; // Declaramos e inicializamos el máximo.
                    //     for ( i = 0; i <= this.RegistradosHoy.length(); i++){
                    //     if (maximo < this.RegistradosHoy.Indice[i]){
                    //         maximo = this.RegistradosHoy.Indice[i];}
                    //         } 
                    //     this.Indice = maximo;
                    //     console.log("Aqui viene el Indice");
                    //     console.log(this.Indice);
                    //     this.Salida();


                    },

      
        
        // Id_Maximo(e){
        //     console.log("ESTAS EN EL METODO MAXIMO ID");
        //     console.log(this.codigo);
        //     console.log(e);
        //     if(e.IntCod  == this.Codigo){
        //       this.RegistradosHoy=this.Recuperando.push(e);
        //       console.log(this.RegistradosHoy);
        //   }
        //     else{
            
        //       } 

        // },
        Salida(){
              if (this.Codig == '') {
                  this.MensajeSalida='Su DNI no se encuentra en la Base de datos'//modal debe ingresar codigo
              }else{
                axios.post('http://192.168.2.71:8080/apiregistro/v1/internos/' + this.Indice + "/" + this.Codig, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    
                        

                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                });
              }
              
          },

        GuardarUsuarioExterno(Codigo){
            axios.post('/apiregistro/v1/externos/'+this.Codigo,
        {
        // DNI=this.DNI
        },
        {headers:{
            'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8' }}
        ).then((response)=>{
            this.DNI='';
            
                }
                )
        },

        Filtro(){ //this.Codigo   00  0 9892399
                // if(this.Codigo.length==10){
                // //Codigo de Alumno o Extrangero
                // this.Codig=this.Codigo.substr(2,this.Codigo.length);
                // this.Busqueda_Codigo();
                // }
                if(this.Codigo.length==8){
                    if(this.Codigo.startsWith("0")){
                        console.log(this.Codigo);
                        if(this.Codigo.startsWith("00")){
                           
                           if(this.Codigo.startsWith("000")){
                               this.Codig=this.Codigo.substring(3,8);
                                console.log(this.Codigo +" codigo quitando 000");
                                this.Busqueda_Codigo(); 
                           }
                           else{
                                this.Codig=this.Codigo.substring(2,8);
                                console.log(this.Codigo +" codigo quitando 00");
                                this.Busqueda_Codigo(); 
                           }
                        }
                        else{
                            this.Codig=this.Codigo.substring(1,8);
                            console.log(this.Codigo +" codigo quitando 0");
                            this.Busqueda_Codigo();
                        }    

                        }   
                    else{
                    this.Codig=this.Codigo;//Codigo de visitante
                    this.Busqueda_Codigo();}
                }
                if(this.Codigo.length==7){
                this.Codig=this.Codigo;//Codigo de Graduado y Docente
                
                this.Busqueda_Codigo();
                }
                
                
                    
        },
        Refrescar(){
            this.dialog = false;
            location.reload();
        },
        // buscarAlumno(){
        // console.log(this.Codig+" este es el codigo de alumno buscado");
        //     axios.get("/apiregistro/v1/usuarios/"+this.Codig,
        //     {headers: { 'content-type': 'application/form-data' }})
        //     .then(response => {
        //       this.alumno = response.data[0];
        //         console.log(this.alumno);
        //         console.log(this.alumno.Nombres);
        //         // this.MostrarAlumno(this.alumno);
        //         // this.Insertar();
                
        //         // eslint-disable-next-line 
                          
        //     })
        //     .catch(e => {
        //         this.errors.push(e);
                
        //     })
        // },
        Busqueda_Codigo_Salida(){
            
            //  this.Codig= this.Codigo.substr(2,this.Codigo.length);
             axios.get("/apiregistro/v1/usuarios/"+this.Codig,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                
                 this.alumnoSalida = response.data[0];
                 console.log(this.alumnoSalida);
                 
                
            })
            
        

        },
        Busqueda_Codigo(){
            
            //  this.Codig= this.Codigo.substr(2,this.Codigo.length);
             axios.get("http://192.168.2.71/apiregistro/v1/usuarios/"+this.Codig,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                
                 this.alumno = response.data[0];
                 console.log(this.alumno);
                 this.Presentable();
                if(response.data.length==0)
                {
                
                    this.Externo=1;
                    console.log(this.Codig+' en metodo BusquedaCodigo');
                    console.log('estas en externo = 1')
                    this.RegistrarUsuarioInterno();
                    
                }
                else{
                    // this.busqueda=true;
                    // this.estado=true;
                    this.Interno=1;
                        console.log(this.Codig+' en metodo BusquedaCodigo');
                        console.log('estas en interno = 1');
                        this.RegistrarUsuarioInterno();
                        
                }
                // this.Insertar();
                
                // eslint-disable-next-line 
                          
            })
            
        

        },
        Presentable(){

                 this.Celular = this.alumno.Celular1+this.Espacio+this.alumno.Celular2+this.Espacio+this.alumno.Celular3;
                 this.Correo = this.alumno.Correo1+this.Espacio+this.alumno.Correo2+this.Espacio+this.alumno.Correo3+this.Espacio+this.alumno.Correo4;
        },
        salir(){
            this.dialogSalida = false;
            this.Codigo='';
            this.$router.push('/');
        },
    

       
    },
    created(){

        
        var myVar = setInterval(myTimer, 1000);

                    function myTimer() {
                    var d = new Date();
                    var t = d.toLocaleTimeString('en-US');
                    document.getElementById("reloj").innerHTML = t 
                    
                    }


    },

   
   
            
}
</script>

<style>


.wrapper {
	overflow: hidden;
	height: 82%;
	position: relative;
}

.cont:before, .cont:after {
	content: "";
	display: table;
	clear: both;
}

/******************************/
/* LOGIN */
/******************************/

.left-layout {
    background-color:#fff;
	width: 42%;
	height: 100%;
	float: left;
	position: absolute;
	/*top: -25%;*/
	left: -7%;
	overflow: hidden;
	-webkit-transform: skewX(-15deg);
	transform: skewX(-15deg);
	-webkit-box-shadow: -37px -5px 9px 44px rgba(0,0,0,0.75);
	-moz-box-shadow: -37px -5px 9px 44px rgba(0,0,0,0.75);
    box-shadow: -37px -5px 9px 44px rgba(0,0,0,0.75);
    z-index: 2;
}

.wrapper-login .left-layout-before {
	position: absolute;
	width: 100%;
	height: 100%;
	/*top: -50%;*/
	left: 14%;
	z-index: -1;
	/* background-image: url(IMG_7889.JPG); */
	/*background-position: 350% 50%;*/
	background-position: 65% 50%;
	background-size: auto 100%;
	background-repeat: no-repeat;
	-webkit-transform: skewX(15deg);
	transform: skewX(15deg);
}

.wrapper-login .left-layout:after {
	content: "";
	position: absolute;
	top: 0;
	right: -1px;
	height: 100%;
	width: 20px;
	background-color: #252525;
}

.right-layout {
	width: 80%;
	height: 100%;
	float: right;
	/* background-image: linear-gradient(
      rgba(255, 255, 255, 0.75),
      rgba(255, 255, 255, 0.75)
    ),url(Derecho.JPG); */
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
}

.wrap-right {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.bg-title-after {
    position: absolute;
    top: 0;
    left: -300%;
    height: 100%;
    width: 200vw;
    background: #252525;
    z-index: -1;
}

/******************************/
/* CARNE */
/******************************/

.wrapper-after-login .left-layout {
	width: 35%;
	left: 0;
	-webkit-transform: none;
	transform: none;
	-webkit-box-shadow: none;
	-moz-box-shadow: none;
	box-shadow: none;
	background-color: #fff;
	display: flex;
	align-items: center;
	justify-content: center;
}

.wrapper-after-login .left-layout:after {
	content: "";
	position: absolute;
	top: 0;
	right: 0px;
	height: 100%;
	width: 5px;
	background-color: #252525;
}

.wrapper-after-login .left-layout .wrapper-foto {
	display: inline-block;
	width: 60%;
}

.wrapper-after-login .left-layout .wrapper-foto img {
	width: 100%;
	height: auto;
}

.wrapper-after-login .right-layout {
	display: flex;
	align-items: center;
	justify-content: flex-end;
}

.wrapper-after-login .right-layout .wrapper-info {
	width: 65vw;
	height: 70%;
	float: right;
	/*background-color: rgba(20,20,20,0.8);*/
	display: flex;
	flex-wrap: nowrap;
	flex-direction: column;
	align-items: center;
}

.wrapper-after-login .right-layout .wrapper-info .small-info {
	padding: 8px 10px 8px 7%;
}

.wrapper-after-login .right-layout .wrapper-info .black-info {
	background-color: #252525;
	color: #fff;
	font-size: 30px;
	width: 100%;
}

.wrapper-after-login .right-layout .wrapper-info .yellow-info {
	background-color: #edbb39;
	color: #252525;
	font-size: 30px;
	width: 100%;
}

.wrapper-after-login .right-layout .wrapper-info .normal-info {
	background-color: transparent;
	color: #252525;
	font-size: 30px;
	width: 100%;
}

.wrapper-after-login .right-layout .wrapper-info .big-info {
	background-color: transparent;
	color: #252525;
	font-size: 70px;
	width: 100%;
	text-align: center;
	height: inherit;
	display: flex;
	align-items: center;
	justify-content: center;
}
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	/* background-color: #1c1c1c; */
	
	color: #ffffff;
	font-size: 16px;
}

.wrap {
	max-width: 1000px;
	width: 90%;
}

.widget {
	margin: 2em;
	width: 40%;
}

.widget p {
	display: inline-block;
	line-height: 1em;
}

.fecha {
	
	font-family: 'Oswald', sans-serif;
	font-size: 1.5em;
	margin-bottom: 5px;
	padding: 20px;
	text-align: center;
	width: 100%;
}

.reloj {
	background-color: rgba(0, 0, 0, 0.5);
	font-family: 'Oswald', sans-serif;
	font-size: 3em;
	padding: 13px;
	text-align: center;
    margin-bottom: -35px;
	width: 100%;
}

.reloj .caja-segundos {
	display: inline-block;
}

.reloj .segundos, .reloj .ampm {
	display: block;
	font-size: 2rem;
}

    
</style>

