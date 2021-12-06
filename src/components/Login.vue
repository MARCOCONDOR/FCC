<template>

<div>
        <!-- <div  :elevation="20" style="height:18%;background-color: #252525" >
   
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXffSRsxD8GWe-wu5pDVEEaDAhEIdu1EBGfw&usqp=CAU" style="height:100%;display:block;margin:auto" >
    </div > -->


<div>

<v-container  >
    <v-layout  >
      <v-flex
        d-flex
      
      >
        <v-img style="margin-right: 90px;height: 700px;width: 859px;"
      src="Bim-Ericsson-Wallet_.jpg"
      :aspect-ratio="16/9"
    >
    </v-img>
    
    
      </v-flex>

        
      
       <v-flex
        d-flex
        
      >
      <div>
          <v-card style="margin-top: 25%;margin-left: 25%;" > 
              
        
        <v-app>
    
                <v-card class="elevation-4" >
                    <v-card-title class="justify-center">
                        <h1>SISTEMA DE PAGOS ECONOMIA</h1>
                    </v-card-title>
                    <v-card-text>
                        <v-alert
                        v-model="alert"
                        dismissible
                        type="warning"
                        transition="scale-transition"
                        >
                        Usuario o contraseña inválido.
                        </v-alert>
                        <v-form @submit="ingresar">
                            <v-text-field name="username" label="Codigo" 
                                        type="text" required :append-icon="'person'" 
                                        v-model="Codigo"
                                        :rules="CodigoRules"
                                        >
                            </v-text-field>
                            <v-text-field name="password" label="Contraseña" 
                                        type="password" required :append-icon="'lock'" 
                                        v-model="password" :rules="passwordRules">
                            </v-text-field>
                            <br>
                            <template >
                            
                            <v-btn  dark  type="submit" block class="white--text" color="blue" @click="ingresar"
                             
                               >
                                Ingresar
                            </v-btn>
                            <v-dialog v-model="dialog" persistent max-width="600px">
                                 
                            <v-card>
                                <v-card-title>
                                <span class="headline">Datos de Usuario</span>
                                </v-card-title>
                                <v-card-text>
                                <v-container grid-list-md>
                                    <v-layout wrap>
                            
                                    <v-flex xs12 >
                                        <v-select
                                         v-model="Sexo"
                                        :items="['Masculino', 'Femenino']"
                                        label="Sexo"
                                        required
                                        :rules="CodigoRules"
                                        ></v-select>
                                    </v-flex>
                                    
                                    <v-flex xs12 >
                                        <v-select
                                         v-model="Escuela"
                                        :items="['E.P. Auditoria Empresarial y del Sector Público', 'E.P. Contabilidad', 'E.P. Gestion Tributaria']"
                                        label="Escuela Profesional"
                                        required
                                        :rules="CodigoRules"
                                        ></v-select>
                                    </v-flex>
                                    <v-flex xs12 >
                                        <v-select
                                         v-model="Ciclo"
                                        :items="['1','2','3','4','5','6','7','8','9','10']"
                                        label="Ciclo de Estudio"
                                        required
                                        :rules="CodigoRules"
                                        ></v-select>
                                    </v-flex>
                                    
                                    </v-layout>
                                </v-container>
                                
                                </v-card-text>
                                <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="blue darken-1" flat @click="dialog = false">Cancelar</v-btn>
                                <v-btn color="blue darken-1" flat @click="Siguiente">Siguiente</v-btn>
                                </v-card-actions>
                            </v-card>
                                </v-dialog>

                            </template>
                            <!-- <template v-slot:activator="{ on, attrs }">
                                <v-btn
                                color="green"
                                dark
                                v-bind="attrs"
                                v-on="on"
                                >
                                Open Persistent
                                </v-btn>
                            </template>     -->

                        </v-form>
                    </v-card-text>
                    <br>      
                </v-card>
            
</v-app> 
  </v-card>
</div>   
      </v-flex>
    </v-layout>
  </v-container>








 <v-dialog v-model="alerta"  max-width="380px">
                                 
                            <v-card>
                                <v-card-title>
                                <span class="headline">BIENVENIDO</span>
                                </v-card-title>
                                
                                <v-card-actions>
                                <v-spacer></v-spacer>
                                <!-- <v-btn color="blue darken-1" flat @click="alert = false">Cancelar</v-btn> -->
                                <v-btn color="blue darken-1" flat @click="Entrar">Ok</v-btn>
                                </v-card-actions>
                            </v-card>
                                </v-dialog>



</div>
</div >


</template>

<script>
import { mapActions } from 'vuex';
import axios from 'axios';

export default {
    name: "Login",
    data(){
        return{
             elevations: [6, 12],
            alerta:false,
            contador:0,
            validacion:[],
            Codig:'',
            Nombre:'',
            Paterno:'',
            Materno:'',
            Semestre:'',
            alumno:[],
            Sexo:'',
            Ciclo:'',
            Escuela:'',
            dialog: false,
            alert: false,
            username: "",
            usernameRules: [
                v => !!v || 'Ingrese un nombre de usuario'
            ],
            Codigo: "",
            CodigoRules: [
                v => !!v || 'Ingrese un codigo de alumno'
            ],
            password: "",
            passwordRules: [
                v => !!v || 'Se requiere la contraseña'
            ]
        }
    },
    created(){
        //console.log(this.$route.path);
        
    },
    computed:{
    },
    methods:{
        Entrar(){
            setTimeout(this.$router.push({
                                    name: "Inicio",
                                    params:{
                                        codigo: this.Codigo,
                                    }
                                    })  , 1000);
        },
        Siguiente(){

            if (this.Sexo == "" || this.Escuela == "" || this.Ciclo == "") {
                

            }else{
                 this.Codig = this.alumno[0].Codigo;
               this.Nombre = this.alumno[0].AL_Nombre;
               this.Paterno=this.alumno[0].AL_Pater;
               this.Materno = this.alumno[0].AL_Mater;
               this.Semestre = this.alumno[0].Semestre;
                
            axios.get('/apiencuesta/v1/alumno/' +this.Codig+'/'+this.Nombre+'/'+this.Paterno+'/'+this.Materno+'/'+this.Sexo+'/'+this.Escuela+'/'+this.Semestre+'/'+this.Ciclo, 
                        {
                        },
                        { headers: {
                            'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                        }
                        })
                        .then((response) => {
                            console.log(response);

                            console.log("Alumno :   "+this.Nombre);
                            
                            // eslint-disable-next-line
                            //console.log(response);
                            
                            // this.Codig='';
                            
                        })
                        .catch(function (error) {
                            // eslint-disable-next-line
                            console.log(error);
                        });
                    
                    
             

                setTimeout(this.$router.push({
                                    name: "Entrada",
                                    params:{
                                        codigo: this.Codigo,
                                    }
                                    })  , 1000);

                       this.dialog=false;     
            }

                      
        },
        Validacion(){
                axios.get("/apipagos/v1/internos/"+this.Codigo,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
              this.validacion = response.data;

            //   this.contador= this.validacion.length;

              if(this.validacion.length!=0){

                                console.log(response.data);
                                    this.mockLogin()
                                     this.dialog=true;
             }
             else{
                 console.log("xddd  ");
                 this.alerta = true;
                 this.mockLogin()
                //   setTimeout(this.$router.push({
                //                     name: "Inicio",
                //                     params:{
                //                         codigo: this.Codigo,
                //                     }
                //                     })  , 1000);
             }
              
              

                           
            })
            .catch(e => {
                this.errors.push(e);
                
            })


                
        },
        ingresar(e){
            e.preventDefault(); //cancela la acción o respuesta por defecto
            if (this.Codigo == "" || this.password == "") {
                this.alert = true;
            }else{
                axios.get("/apipagos/v1/empleados/"+this.Codigo,
                {headers: { 'content-type': 'application/form-data' }})
                .then(response => {
                    //console.log(response.data.length);
                    console.log("la toxica");

                    if (response.data.length == 0) {
                        this.alert = true;
                    }else{
                            this.alumno=response.data;
                        if( this.Codigo==this.alumno[0].Codigo && this.password == this.alumno[0].contrasena ){
                                console.log("contraseña ok");
                                this.Validacion();

                                    

                        }else{
                                this.alert = true;

                        }

                        
                        

                        
                        //variable local
                        // let usuario = {         
                        //     cargo: "Administrador",
                        //     nombre: response.data[0].nombres,
                        //     a_paterno: response.data[0].a_paterno,
                        //     username: response.data[0].usuario
                        // }
                        //guarda en variable global-->store.js
                        // this.actualizarUsuario(usuario);
                        // console.log("entrando a la ruta /")
                        // this.mockLogin()
                        // // setTimeout(function(){ location.href = '/#/Entrada' }, 1000);
                        // this.dialog=true;
                        
                        // redirecciona a inicio
                        // location.href = '/#/Entrada'
                        // this.$router.push({
                        //             name: "Entrada",
                        //             params:{
                        //                 codigo: this.Codigo,
                        //             }
                        //             });    
                        // this.$router.push('/Entrada');
                    }
                })
                .catch(e => {
                    // eslint-disable-next-line 
                    console.log(e);
                    this.alert = true;    
                })
            }
        },
        ...mapActions(['mockLogin']),
    //     ingresar(){
    //             if (this.username == "Admin" || this.password == "159"){
    //                 console.log("entrando a la ruta /")
    //     //                 //redirecciona a inicio
    //     //                 // location.href = '/Entrada'
    //     //                 // // this.$router.push({
    //     //                 // //             name: "Entrada"
    //     //                 // //             // params:{
    //     //                 // //             //     codigo: this.Codig,
    //     //                 // //             // }
    //     //                 // //             });    
    //                     this.$router.push('/Tablas');
    //             }else{
    //                 this.alert = true;
    //     }
    // }
      }      }
</script>


<style>

.container {
    max-width: 1500px;
}
    
</style>




