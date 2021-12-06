
<template>
 <div>



  <div id="app">
     <v-app id="inspire1" > 
     <v-card 
    color="#738ee5"
    dark
  >
    <v-card-title   style="background-color: #4CAF50;">
    Reporte General por Ciclo
    </v-card-title>
    <v-card-text>
      Busqueda por Ciclo
     
    </v-card-text>
    <v-card-text>
       <v-autocomplete
                                v-model="Semestre_Elegido"
                                :items="this.Sem"
                                label="Ingrese el Ciclo"
                                prepend-icon="account_circle"
                                color="green"
                                full-width
                                solo
                                hint="Buscando datos.."
                                
                              >
                              </v-autocomplete>
                              <div class="my-2">
                              <v-btn
                                color="warning"
                                large
                                dark
                                @click="Mostrar_Datos"
                              >
                                <v-icon>account_circle</v-icon>Buscar 
                              </v-btn>
                              </div>
    </v-card-text>
    <v-divider></v-divider>
    
    
  </v-card>
  </v-app>

  </div>



  <div>


  
  
  <v-data-table 
    
    id="tblData" 
    :headers="headers"
    :items="marco"
    class="elevation-3"
    hide-actions
    
  > 
    
    <template v-slot:items="props"  >
      <td>{{ props.index + 1 }}</td>
      <td class="text-xs-left">{{ props.item.Alumno }}</td>
      <td class="text-xs-center">{{ props.item.DNI }}</td>
      <td class="text-xs-center">{{ props.item.THaber }}</td>
      <td class="text-xs-center">{{ props.item.TFechaPago }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher }}</td>
     <td class="text-xs-center">{{ props.item.THaber1 }}</td>
      <td class="text-xs-center">{{ props.item.TFechaPago1 }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher1 }}</td>
      <td class="text-xs-center">{{ props.item.THaber2 }}</td>
      <td class="text-xs-center">{{ props.item.TFechaPago2 }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher2 }}</td>
      <td class="text-xs-center">{{ props.item.THaber3 }}</td>
      <td class="text-xs-center">{{ props.item.TFechaPago3 }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher3 }}</td>
       <td class="text-xs-center">{{ props.item.THaber4 }}</td>
      <td class="text-xs-center">{{ props.item.TFechaPago4 }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher4 }}</td>
      <td class="text-xs-center">{{ props.item.TVoucher4 }}</td>
      <td class="text-xs-center">{{ props.item.THaber+props.item.THaber1+props.item.THaber2+props.item.THaber3+props.item.THaber4 }}</td>

    </template>
  </v-data-table>
  </div>

  <button style="background-color:green" @click="exportTableToExcel('tblData')">DESCARGAR TABLA</button>
</div>
  
</template>


<script>
import axios from 'axios';  
  export default {

    data () {
      return {
        Semestre_Elegido: '',
        Sem:[],
        Codigo1:'',
        Codigo:48284572,
        Semestre:'20-1',
        Cero:'20-1',
        Cerosss:'20-1',
        i:0,
        temporal:[],
        datos:[],
        marco:[],
        alumno:[ 

          { Alumno:[],historial  :[]  },
          { Alumno:[],historial :[] },
          { Alumno:[],historial  :[]  },
          { Alumno:[],historial :[] },
          { Alumno:[],historial  :[]  },
          { Alumno:[],historial :[] },
          { Alumno:[],historial  :[]  },
          { Alumno:[],historial :[] },
          { Alumno:[],historial  :[]  },
          { Alumno:[],historial :[] },

          ],
        headers: [
          {
            text: 'N',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Alumno', value: 'Alumno' , sortable: false ,position:'center'},
          { text: 'DNI', value: 'Codigo', sortable: false  },
          { text: 'MATRICULA', value: 'THaber' },
          { text: 'FECHA PAGO', sortable: false   },
          { text: 'VOUCHER',sortable: false   },
          { text: '1ERA PENSION', sortable: false   },
          { text: 'FECHA PAGO', sortable: false  },
          { text: 'VOUCHER', sortable: false   },
          { text: '2DA PENSION', sortable: false   },
          { text: 'FECHA PAGO', sortable: false   },
          { text: 'VOUCHER', sortable: false  },
          { text: '3RA PENSION', sortable: false   },
          { text: 'FECHA PAGO', sortable: false   },
          { text: 'VOUCHER', sortable: false   },
          { text: '4TA PENSION', sortable: false   },
          { text: 'FECHA PAGO', sortable: false   },
          { text: 'VOUCHER', sortable: false   },
          { text: 'DEBE', sortable: false  },
          { text: 'HABER', sortable: false  },
          { text: 'SALDO', sortable: false   }
        ],
        
      }
    },
    methods: {
       exportTableToExcel(tableID, filename = ''){
          var downloadLink;
          var dataType = 'application/vnd.ms-excel';
          var tableSelect = document.getElementById(tableID);
          var tableHTML = tableSelect.outerHTML.replace(/ /g, '%20');
          
          // Specify file name
          filename = filename?filename+'.xls':'excel_data.xls';
          
          // Create download link element
          downloadLink = document.createElement("a");
          
          document.body.appendChild(downloadLink);
          
          if(navigator.msSaveOrOpenBlob){
              var blob = new Blob(['\ufeff', tableHTML], {
                  type: dataType
              });
              navigator.msSaveOrOpenBlob( blob, filename);
          }else{
              // Create a link to the file
              downloadLink.href = 'data:' + dataType + ', ' + tableHTML;
          
              // Setting the file name
              downloadLink.download = filename;
              
              //triggering the function
              downloadLink.click();
          }
        },

      Mostrar_Datos(){
        console.log(this.Sem);
        this.Cero=this.Semestre_Elegido;
        this.Semestre=this.Semestre_Elegido;
        console.log(this.Semestre);
        console.log(this.Cero);
        this.TraerAlumno();

      },

      TraerSemestre(){

             axios.get("/apipagos/v1/Semestres/"+this.Cerosss,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                

                this.Semestre = response.data;
                console.log(this.Semestre);

                this.Semestre.forEach(Semestre=>{
                  this.Sem.push(Semestre.Semestre);
                  console.log("el semestres es : "+this.Sem);
                   

                  
                  
                  })
                
               
            })
      },

     
      TraerAlumno(){

             axios.get("/apipagos/v1/alumno/"+this.Cero,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                

                this.marco = response.data;
               

                this.marco.forEach(marco=>{
                  this.Codigo=marco.DNI;
                  console.log("el codigo es : "+this.Codigo);
                    this.Traer_Datos_Ciclo_Matricula();

                  
                  
                  })

                        



              

                 


                 

                
               
            })
      },
      Traer_Datos_Ciclo_Matricula(){
              console.log(this.Codigo);
             axios.get("/apipagos/v1/tablageneral/"+this.Codigo+'/'+this.Semestre,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                this.datos = response.data;
                console.log("los datos extraidos son: " +this.i+" y este su numero de busqueda");
                console.log(this.datos);
                if(this.datos == ''){
                  console.log(this.Codigo);
                this.marco[this.i].TConcepto='';
                 this.marco[this.i].TFechaPago='';
                 this.marco[this.i].THaber='';
                 this.marco[this.i].TVoucher= '';
                 this.marco[this.i].TConcepto1='';
                 this.marco[this.i].TFechaPago1='';
                 this.marco[this.i].THaber1='';
                 this.marco[this.i].TVoucher1= '';
                  this.marco[this.i].TConcepto2='';
                 this.marco[this.i].TFechaPago2='';
                 this.marco[this.i].THaber2='';
                 this.marco[this.i].TVoucher2= '';
                  this.marco[this.i].TConcepto3='';
                 this.marco[this.i].TFechaPago3='';
                 this.marco[this.i].THaber3='';
                 this.marco[this.i].TVoucher3= '';
                  this.marco[this.i].TConcepto4='';
                 this.marco[this.i].TFechaPago4='';
                 this.marco[this.i].THaber4='';
                 this.marco[this.i].TVoucher4= '';
                 
                 this.i = this.i +1;

                }
                else{
                 
                

                 this.marco[this.i].TConcepto=this.datos[0].TConcepto;
                 this.marco[this.i].TFechaPago=this.datos[0].TFecha_Pago;
                 this.marco[this.i].THaber=parseInt(this.datos[0].THaber);
                 this.marco[this.i].TVoucher= this.datos[0].TVoucher;
                //  console.log("el dni : "+this.Codigo+"valoress de primer pagoooooo"+this.datos[0]);
                        if(this.datos[1] == null){
                        this.marco[this.i].TConcepto1='';
                        this.marco[this.i].TFechaPago1='';
                        this.marco[this.i].THaber1=0;
                        this.marco[this.i].TVoucher1= ''; 

                        }
                        else{
                        this.marco[this.i].TConcepto1=this.datos[1].TConcepto;
                        this.marco[this.i].TFechaPago1=this.datos[1].TFecha_Pago;
                        this.marco[this.i].THaber1=parseInt(this.datos[1].THaber);
                        this.marco[this.i].TVoucher1= this.datos[1].TVoucher;
                        //  console.log("el dni : "+"valoress de segundo pagoooooo"+this.datos[1]); 

                                if(this.datos[2] == null){
                                    this.marco[this.i].TConcepto2='';
                                    this.marco[this.i].TFechaPago2='';
                                    this.marco[this.i].THaber2=0;
                                    this.marco[this.i].TVoucher2= '';

                                }
                                else{

                                  this.marco[this.i].TConcepto2=this.datos[2].TConcepto;
                                  this.marco[this.i].TFechaPago2=this.datos[2].TFecha_Pago;
                                  this.marco[this.i].THaber2=parseInt(this.datos[2].THaber);
                                  this.marco[this.i].TVoucher2= this.datos[2].TVoucher;
                                  //  console.log("el dni : "+"valoress de tercer pagoooooo"+this.datos[2]);    

                                        if(this.datos[3] == null){
                                                this.marco[this.i].TConcepto3='';
                                                this.marco[this.i].TFechaPago3='';
                                                this.marco[this.i].THaber3=0;
                                                this.marco[this.i].TVoucher3= '';

                                          }
                                          else{

                                              this.marco[this.i].TConcepto3=this.datos[3].TConcepto;
                                              this.marco[this.i].TFechaPago3=this.datos[3].TFecha_Pago;
                                              this.marco[this.i].THaber3=parseInt(this.datos[3].THaber);
                                              this.marco[this.i].TVoucher3= this.datos[3].TVoucher;
                                              //  console.log("el dni : "+"valoress de cuarto pagoooooo"+this.datos[3]);   

                                                            if(this.datos[4] == null){
                                                                  this.marco[this.i].TConcepto4='';
                                                                  this.marco[this.i].TFechaPago4='';
                                                                  this.marco[this.i].THaber4=0;
                                                                  this.marco[this.i].TVoucher4= '';

                                                              }
                                                              else{

                                                                   this.marco[this.i].TConcepto4=this.datos[4].TConcepto;
                                                                  this.marco[this.i].TFechaPago4=this.datos[4].TFecha_Pago;
                                                                  this.marco[this.i].THaber4=parseInt(this.datos[4].THaber);
                                                                  this.marco[this.i].TVoucher4= this.datos[4].TVoucher;
                                                                  //  console.log("el dni : "+"valoress de quinto pagoooooo"+this.datos[4]);

                                        


                                                              } 
                                


                                          } 
                          


                                }    


                        }
                 
                 
                
                 
                 
                 this.i = this.i +1;
                 console.log("contador va en "+ this.i);
                 console.log(this.marco);
                }
                //  console.log(this.alumno.Alumno[0]);
                //  this.alumno[0].historial.push(this.datos);
                //  console.log(this.alumno[0]);
                  
                //  this.datos.forEach(datos=>{
                // this.alumno[0].push(datos);
                // console.log(this.alumno);
                
                
                //  })

               
            })
      },
    },

    created() {
      this.TraerSemestre();
      // this.TraerAlumno();
      // this.Traer_Datos_Ciclo_Matricula();
    },

  }
</script>
<style>
.v-table__overflow {
    
    height: 1000px !important;
    /* width: 992px; */
}
  
</style>