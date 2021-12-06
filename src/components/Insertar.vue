<template>
<div>
  <div id="app">
     <v-app id="inspire1" > 
     <v-card 
    color="#738ee5"
    dark
  >
    <v-card-title   style="background-color: #4CAF50;">
      Registro de Pagos Por Alumno
    </v-card-title>
    <v-card-text>
      Busqueda por DNI E Intervalo de Ciclos
     
    </v-card-text>
    <v-card-text>
       <v-autocomplete
                                v-model="Codigo"
                                :items="this.Codigos"
                                label="Ingrese DNI del Alumno"
                                prepend-icon="account_circle"
                                color="green"
                                full-width
                                solo
                                hint="Buscando Codigo.."
                                
                              >
                              </v-autocomplete>
                              <div class="my-2">
                              <v-btn
                                color="warning"
                                large
                                dark
                                @click="Mostrar_Datos"
                              >
                                <v-icon>account_circle</v-icon>Buscar Alumno
                              </v-btn>
                              </div>
    </v-card-text>
    <v-divider></v-divider>
    <v-expand-transition>
      <v-list v-if="model" style="background-color: #5f56ec;">
                    <v-form>
                <v-container>
                  <v-layout row wrap>

                    <v-flex xs12 sm6>
                      <v-text-field
                         v-model="CODIGO"
                        
                        label="Codigo"
                        box
                        disabled
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm6>
                      <v-text-field
                         v-model="NOMBRES_APELLIDOS"
                        label="Alumno"
                        box
                        disabled
                      ></v-text-field>
                    </v-flex>

                   <v-flex xs12 sm6>
                      <v-text-field
                         v-model="MAESTRIA"
                        label="Maestria"
                        box
                        disabled
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm6>
                      <v-text-field
                         v-model="COD_ESP"
                        label="Especialidad"
                        box
                        disabled
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm6>
                      <v-text-field
                        v-model="DNI"
                        label="DNI"
                        box
                        disabled
                      ></v-text-field>
                    </v-flex>

                    
                   

                  </v-layout>
                </v-container>
              </v-form>
        </v-list> 
      <!-- <v-list v-if="model" class="red lighten-3">
        <v-list-tile
          v-for="(field, i) in fields"
          :key="i"
        >
          <v-list-tile-content>
            <v-list-tile-title v-text="field.value"></v-list-tile-title>
            <v-list-tile-sub-title v-text="field.key"></v-list-tile-sub-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list> -->
    </v-expand-transition>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        :disabled="!model"
        color="grey darken-3"
        @click="model = null"
      >
        OCULTAR
        <v-icon right>mdi-close-circle</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
  </v-app>

  </div>
  <div>
    <!-- <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="dialogo_AGREGAR_Registro=!dialogo_AGREGAR_Registro"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn> -->
    <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Mostrar_Registros_Tablas"
      
    >
      Mostrar Registro de Pagos
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
    <v-dialog  v-model="dialogo_AGREGAR_Registro" max-width="800px" >




     <v-card
    class="mx-auto"
    
  >
    <v-card-title>
      <h2 class="text-h4">
        Alumno
      </h2>
      <v-spacer></v-spacer>
      <span class="text-h6">{{this.fecha}}</span>
    </v-card-title>

    <v-card-text>
      <span>{{this.CODIGO}} </span>
      <br>
      <span>{{this.NOMBRES_APELLIDOS}} </span> <br>
      Seleccione el Semestre y luego dar click
      
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-text>
      <span class="subheading">Seleccione el Semestre</span>

      <!-- <v-chip-group
        v-model="selection"
        active-class="deep-purple--text text--accent-4"
        mandatory
      >
        <v-chip>Extra Soft</v-chip>
        <v-chip>Soft</v-chip>
        <v-chip>Medium</v-chip>
        <v-chip>Hard</v-chip>
      </v-chip-group> -->
                           <v-autocomplete
                                v-model="Semestre_Seleccionado"
                                :items="this.Sem"
                                label="Semestre"
                                prepend-icon="account_circle"
                                color="green"
                                full-width
                                solo
                                hint="Random set of categories"
                              >
                              </v-autocomplete>
      
    </v-card-text>


    <v-card-actions>
      <v-btn
        block
        class="white--text"
        color="deep-purple accent-4"
        @click="dialogo_Semestre=!dialogo_Semestre"
      >
        SIGUIENTE
      </v-btn>
    </v-card-actions>
  </v-card>
                            </v-dialog>
<!-- Aqui empieza v-model semetre                             -->
  <v-dialog  v-model="dialogo_Semestre">

                      <v-stepper v-model="e6" vertical>
                        <div >
                        <v-card  class="step1"> <span style="padding-left: 710px;"></span >  {{this.Semestre_Seleccionado}} </v-card>
                        <v-card  class="step1"> <span style="padding-left: 620px;"></span >  {{this.NOMBRES_APELLIDOS}} </v-card>
                        <v-card  class="step1"> <span style="padding-left: 700px;"></span >  {{this.CODIGO}} </v-card>
                       </div>
                    <v-stepper-step :complete="e6 > 1" step="1">
                      Matricula
                      <small>Datos de Pago</small>
                    </v-stepper-step>

                    <v-stepper-content step="1">
                      <v-card color="grey lighten-1" class="mb-5" height="200px">
                                      <v-form  style="background-color: greenyellow;">
                                        <v-container>
                                          <v-layout>
                                          <v-flex xs6 md8>
                                             
                                                  <v-menu
                                                  
                                                    ref="menu"
                                                    v-model="menu"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="date"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="date"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="date"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu.save(date)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>
                                             
                                              
                                               
                                              <v-text-field
                                                v-model="VOUCHER"
                                                label="VOUCHER"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="DEBE"
                                                label="DEBE"
                                                required
                                              ></v-text-field>
                                            </v-flex>
                                            <v-flex
                                              xs6
                                              md8
                                            >
                                            <v-menu
                                                  
                                                    ref="menu2"
                                                    v-model="menu2"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="datofin"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="datofin"
                                                        label="Fecha Fin"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="datofin"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu2 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu2.save(datofin)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>
                                            <v-text-field
                                                v-model="BF"
                                                label="BOLETA/FACTURA"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="HABER"
                                                label="HABER"
                                                required
                                              ></v-text-field>
                                              </v-flex>
                                              </v-layout>
                                          </v-container>
                                      </v-form>
                      </v-card>
                      <v-btn color="primary" @click="e6 = 2">Continue</v-btn>
                      <v-btn flat>Cancel</v-btn>
                    </v-stepper-content>

                    <v-stepper-step :complete="e6 > 2" step="2">Pension: Primera Cuota</v-stepper-step>

                    <v-stepper-content step="2">
                      <v-card color="grey lighten-1" class="mb-5" height="200px">
                        <v-form  style="background-color: greenyellow;">
                                        <v-container>
                                          <v-layout>
                                          <v-flex xs6 md8>
                                              
                                              <v-menu
                                                  
                                                    ref="menu3"
                                                    v-model="menu3"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="date2"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="date2"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="date2"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu3 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu3.save(date2)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>
                                             




                                              <v-text-field
                                                v-model="VOUCHER2"
                                                label="VOUCHER"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="DEBE2"
                                                label="DEBE"
                                                required
                                              ></v-text-field>
                                            </v-flex>
                                            <v-flex
                                              xs6
                                              md8
                                            >
                                            
                                             <v-menu
                                                  
                                                    ref="menu4"
                                                    v-model="menu4"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="datofin2"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="datofin2"
                                                        label="Fecha Fin"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="datofin2"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu4 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu4.save(datofin2)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>





                                            <v-text-field
                                                v-model="BF2"
                                                label="BOLETA/FACTURA"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="HABER2"
                                                label="HABER"
                                                required
                                              ></v-text-field>
                                              </v-flex>
                                              </v-layout>
                                          </v-container>
                                      </v-form>
                      </v-card>
                      <v-btn color="primary" @click="e6 = 3">Continue</v-btn>
                      <v-btn flat>Cancel</v-btn>
                    </v-stepper-content>

                    <v-stepper-step :complete="e6 > 3" step="3">Pension: Segunda Cuota</v-stepper-step>

                    <v-stepper-content step="3">
                      <v-card color="grey lighten-1" class="mb-5" height="200px">
                        <v-form  style="background-color: greenyellow;">
                                        <v-container>
                                          <v-layout>
                                          <v-flex xs6 md8>
                                              
                                               <v-menu
                                                    ref="menu5"
                                                    v-model="menu5"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="date3"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        v-model="date3"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="date3"
                                                      no-title
                                                      scrollable>
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu5 = false">
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      @click="$refs.menu5.save(date3)">
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>



                                              <v-text-field
                                                v-model="VOUCHER3"
                                                label="VOUCHER"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="DEBE3"
                                                label="DEBE"
                                                required
                                              ></v-text-field>
                                            </v-flex>
                                            <v-flex
                                              xs6
                                              md8
                                            >
                                            
                                            <v-menu
                                                  
                                                    ref="menu6"
                                                    v-model="menu6"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="datofin3"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="datofin3"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="datofin3"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu6 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu6.save(datofin3)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>





                                            <v-text-field
                                                v-model="BF3"
                                                label="BOLETA/FACTURA"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="HABER3"
                                                label="HABER"
                                                required
                                              ></v-text-field>
                                              </v-flex>
                                              </v-layout>
                                          </v-container>
                                      </v-form>
                      </v-card>
                      <v-btn color="primary" @click="e6 = 4">Continue</v-btn>
                      <v-btn flat>Cancel</v-btn>
                    </v-stepper-content>

                    <v-stepper-step :complete="e6 > 4" step="4">Pension: Tercera Cuota</v-stepper-step>

                    <v-stepper-content step="4">
                      <v-card color="grey lighten-1" class="mb-5" height="200px">
                        <v-form  style="background-color: greenyellow;">
                                        <v-container>
                                          <v-layout>
                                            <v-flex xs6 md8>
                                          
                                              <v-menu
                                                  
                                                    ref="menu7"
                                                    v-model="menu7"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="date4"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="date4"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="date4"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu7 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu7.save(date4)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>





                                              <v-text-field
                                                v-model="VOUCHER4"
                                                label="VOUCHER"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="DEBE4"
                                                label="DEBE"
                                                required
                                              ></v-text-field>
                                            </v-flex>
                                            <v-flex
                                              xs6
                                              md8
                                            >

                                            <v-menu
                                                  
                                                    ref="menu8"
                                                    v-model="menu8"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="datofin4"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="datofin4"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="datofin4"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu8 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu8.save(datofin4)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>


                                            <v-text-field
                                                v-model="BF4"
                                                label="BOLETA/FACTURA"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="HABER4"
                                                label="HABER"
                                                required
                                              ></v-text-field>
                                              </v-flex>
                                              </v-layout>
                                          </v-container>
                                      </v-form>
                      </v-card>
                      <v-btn color="primary" @click="e6 = 5">Continue</v-btn>
                      <v-btn flat>Cancel</v-btn>
                    </v-stepper-content>

                    <v-stepper-step step="5">Pension: Cuarta Cuota</v-stepper-step>
                    <v-stepper-content step="5">
                      <v-card color="grey lighten-1" class="mb-5" height="200px">
                        <v-form  style="background-color: greenyellow;">
                                        <v-container>
                                          <v-layout>
                                          <v-flex xs6 md8>
                                              
                                              <v-menu
                                                  
                                                    ref="menu9"
                                                    v-model="menu9"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="date5"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="date5"
                                                        label="Fecha inicio"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="date5"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu9 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu9.save(date5)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>




                                              <v-text-field
                                                v-model="VOUCHER5"
                                                label="VOUCHER"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="DEBE5"
                                                label="DEBE"
                                                required
                                              ></v-text-field>
                                            </v-flex>
                                            <v-flex
                                              xs6
                                              md8
                                            >
                                              <v-menu
                                                  
                                                    ref="menu10"
                                                    v-model="menu10"
                                                    :close-on-content-click="false"
                                                    :return-value.sync="datofin5"
                                                    transition="scale-transition"
                                                    offset-y
                                                    min-width="auto"
                                                  >
                                                    <template v-slot:activator="{ on, attrs }">
                                                      <v-text-field
                                                        
                                                        v-model="datofin5"
                                                        label="Fecha Fin"
                                                        prepend-icon="event"
                                                        readonly
                                                        v-bind="attrs"
                                                        v-on="on"
                                                      
                                                      ></v-text-field>
                                                    </template>
                                                    <v-date-picker
                                                      v-model="datofin5"
                                                      no-title
                                                      scrollable
                                                      
                                                    >
                                                      <v-spacer></v-spacer>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                        @click="menu10 = false"
                                                      >
                                                        Cancel
                                                      </v-btn>
                                                      <v-btn
                                                        style="background-color: green;"
                                                        text
                                                        color="primary"
                                                      
                                                        @click="$refs.menu10.save(datofin5)"
                                                      
                                                        
                                                      >
                                                        OK
                                                      </v-btn>
                                                    </v-date-picker>
                                                  </v-menu>




                                            <v-text-field
                                                v-model="BF5"
                                                label="BOLETA/FACTURA"
                                                required
                                              ></v-text-field>
                                              <v-text-field
                                                v-model="HABER5"
                                                label="HABER"
                                                required
                                              ></v-text-field>
                                              </v-flex>
                                              </v-layout>
                                          </v-container>
                                      </v-form>
                      </v-card>
                      <v-btn color="primary" @click="e6 = 1">Continue</v-btn>
                      <v-btn flat>Cancel</v-btn>
                    </v-stepper-content>
                    <v-btn color="primary"  @click="Ingresar_Datos">Guardar Datos</v-btn>
                  </v-stepper>
    </v-dialog>                            
  
                            
  </div>



  <v-expand-transition>
    
   <v-container  v-if="modelC" fluid grid-list-md  style="max-width: 1520px">

     <v-flex v-if="R_0" v-for="registro in 1"  :key="registro.id" >
       <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[0] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table  
    id="tblData" 
    hide-default-header="true"
    hide-default-footer="true"
    disable-pagination
    :headers="headers"
    :items="registros[0].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->

        <td class="text-xs-right">{{  0 }}</td>   
         <!-- aqui arriba dias -->
  
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
      <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=0)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>
  </v-data-table>
  <div>
     <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=0)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  <!-- <button class="ma-2" style="background-color: blue;"
      color="success" @click="GuardarDato1">Guardar Datos</button> -->
      
  </div>
  </v-flex>


   <v-flex v-if="R_1" v-for="registro in 1"  :key="registro.id" >
    <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[1] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table 
    id="tblData2"  
    :headers="headers"
    :items="registros[1].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->
          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
        <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=1)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>
  </v-data-table>
  <div>
   <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=1)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </div>
  </v-flex>






   <v-flex v-if="R_2" v-for="registro in 1" :key="registro.id" >
     <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[2] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div> 
    <v-data-table  
    id="tblData3"  
    :headers="headers"
    :items="registros[2].historial"
    class="elevation-15"
  >
      <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->
          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
        <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=2)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>






  </v-data-table>
       <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=2)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
    <v-spacer></v-spacer>
        
  </v-flex>


   <v-flex v-if="R_3" v-for="registro in 1" :key="registro.id" >
      <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[3] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table 
    id="tblData4"   
    :headers="headers"
    :items="registros[3].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->

          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
        <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=3)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>




  </v-data-table>
         <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=3)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </v-flex>

  <v-flex v-if="R_4" v-for="registro in 1" :key="registro.id" >
     <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[4] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table 
    id="tblData5"   
    :headers="headers"
    :items="registros[4].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->
          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
        <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=4)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>


  </v-data-table>
         <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=4)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </v-flex>


  <v-flex v-if="R_5" v-for="registro in 1" :key="registro.id" >
      <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[5] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table 
    id="tblData6"   
    :headers="headers"
    :items="registros[5].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->

          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

        
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
         <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=5)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>




  </v-data-table>
         <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=5)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </v-flex>

  <v-flex v-if="R_6" v-for="registro in 1" :key="registro.id" >
      <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[6] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table 
    id="tblData7"   
    :headers="headers"
    :items="registros[6].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->

          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=6)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>




  </v-data-table>
         <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=6)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </v-flex>



  <v-flex v-if="R_7" v-for="registro in 1" :key="registro.id" >
      <div>
       <v-toolbar-title style="color: blue;"> {{ semestres[7] }}   <v-btn  color="primary" dark class="mb-2" >Nuevo Pago</v-btn> </v-toolbar-title>
        </div>
    <v-data-table  
    id="tblData8"  
    :headers="headers"
    :items="registros[7].historial"
    class="elevation-15"
  >
    <template v-slot:items="props">
      <template >
     <td> <v-edit-dialog
          :return-value.sync="props.item.Semestre"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.Semestre }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.Semestre"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td> </template>
      <!-- <v-text-field v-model="datofin4" label="Fecha inicio" prepend-icon="event" readonly v-bind="attrs" v-on="on"></v-text-field> -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Vencimiento"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Vencimiento }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Vencimiento"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
      <!-- Tercera -->
      <template >
      <td> <v-edit-dialog
          :return-value.sync="props.item.TFecha_Pago"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TFecha_Pago }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TFecha_Pago"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Cuarto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TVoucher"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TVoucher }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TVoucher"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Quinto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TBole_Factura"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TBole_Factura }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TBole_Factura"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        
        <!-- Sexto -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TConcepto"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TConcepto }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TConcepto"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>
        <!-- Datos estaticos -->

          <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
        <!-- Septimo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.TDebe"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.TDebe }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.TDebe"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td></template>

         
        <!-- Octavo -->
        <template >
        <td> <v-edit-dialog
          :return-value.sync="props.item.THaber"
          @save="save"
          @cancel="cancel"
          @open="open"
          @close="close"
        >
          {{ props.item.THaber }}
          <template v-slot:input>
            <v-text-field
              v-model="props.item.THaber"
              :rules="[max25chars]"
              label="Edit"
              single-line
              counter
            ></v-text-field>
          </template>
        </v-edit-dialog></td>
        <td class="text-xs-right">{{ props.item.THaber-props.item.TDebe }}</td>
         <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="GuardarFila(valor=props.index,pos=7)"
          >
            save
          </v-icon>
          <v-icon
            small
            @click="EliminarFila"
          >
            delete
          </v-icon>
        </td>
        </template>
     
    </template>




  </v-data-table>
         <v-btn
      class="ma-2"
      :loading="loading2"
      :disabled="loading2"
      color="success"
      @click="Insertar_Registro(pos=7)"
      
    >
      Ingresar Nuevo Registro
      <template v-slot:loader>
        <span>Loading...</span>
      </template>
    </v-btn>
  </v-flex>    








    <div  center class="my-2">
            <v-btn
              x-large
              color="success"
              dark
              @click="Activar_Tabla"
            >
              AGREGAR TABLA DE PAGOS
            </v-btn>
             <button style="background-color:green" @click="exportTableToExcel('tblData','tblData2','tblData3','tblData4','tblData5','tblData6','tblData7','tblData8')">DESCARGAR TABLAS</button>
              
          </div>

   </v-container> 


   </v-expand-transition>





   </div>

</template>
<script>
 
import axios from 'axios';  
  export default {
    
   data () {
    
      return {
        SError :'-',
        valor:150,
        k:0,
        x:0,
        y:0,
        z:0,
        w:0,
        a1:0,
        a2:0,
        a3:0,
        a4:0,
        dialog_nfila:false,
        pos:120,
        n:0,
        snack: false,
        snackColor: '',
        snackText: '',
        max25chars: v => v.length <= 100 || 'Input too long!',
        pagination: {},
        R_0:false,
        R_1:false,
        R_2:false,
        R_3:false,
        R_4:false,
        R_5:false,
        R_6:false,
        R_7:false,
        Concepto5:'Pension: Cuarta Cuota',
        Concepto4:'Pension: Tercera Cuota',
        Concepto3:'Pension: Segunda Cuota',
        Concepto2:'Pension: Primera Cuota',
        Concepto1:'Matricula',
        modelC:false,
        numero:0,
        Numero_Tabla:[],
        Concepto:'Matricula',
        HABER5:'',
        HABER4:'',
        HABER3:'',
        HABER2:'',
        HABER:'',
        DEBE5:'',
        DEBE4:'',
        DEBE3:'',
        DEBE2:'',
        DEBE:'',
        BF5:'',
        BF4:'',
        BF3:'',
        BF2:'',
        BF:'',
        VOUCHER5:'',
        VOUCHER4:'',
        VOUCHER3:'',
        VOUCHER2:'',
        VOUCHER:'',
        Semestre_Seleccionado:'',
        DNI:'',
        COD_ESP:'',
        NOMBRES_APELLIDOS:'',
        CODIGO:'',
        MAESTRIA:'',
        firstname: '',
        menu10:false,
        menu9: false,
        menu8:false,
        menu7: false,
        menu6:false,
        menu5: false,
        menu4:false,
        menu3: false,
        menu2:false,
        menu: false,
        datofin5: new Date().toISOString().substr(0, 10),
        datofin4: new Date().toISOString().substr(0, 10),
        datofin3: new Date().toISOString().substr(0, 10),
        datofin2: new Date().toISOString().substr(0, 10),
        datofin: new Date().toISOString().substr(0, 10),
        date5: new Date().toISOString().substr(0, 10),
        date4: new Date().toISOString().substr(0, 10),
        date3: new Date().toISOString().substr(0, 10),
        date2: new Date().toISOString().substr(0, 10),
        date: new Date().toISOString().substr(0, 10),
        fecha:new Date().toISOString().substr(0, 10),
        e6: 1,
         selection: 2,
        dialogo_Semestre:false,
        dialogo_AGREGAR_Registro:false,
        loader: null,
        loading2: false,
        model:false,
        Codigos:[],
        semestres:[],
        Cero:0,
          cadena_codigos:[],
          cadena_Alumno:[],
          Codigo:'',
          ayuda:'152',
          ayuda1:'152',
          TCodigo:'19117023',
          Semestre:'19-1',
          Semestre2:'19-2',
          historial:[],
          historial2:[],
          historial3:[],
          contador:0,
          nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters'
      ],
        registros:[ 

          { id:1,historial  :[]  },
          { id:2,historial :[] },
          { id:3,historial :[] },
          { id:4,historial :[] },
          { id:5,historial :[] },
          { id:6,historial :[] },
          { id:7,historial :[] },
          { id:8,historial :[] },

          ],
          Controlador: [{Re1:0,Re2:0,Re3:0,Re4:0,Re5:0}],
          improvisados:[
              {Indice: '1',Semestre: '0',TBole_Factura:'0',TCodigo: '0',TConcepto: 'Matricula',TDebe: '0',TFecha_Pago: '0',TFecha_Vencimiento: '0',THaber: '0',TVoucher: '0',nv:0},

          ],
          improvisados1:
              {Indice: '2',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Primera Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados2:
              {Indice: '3',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Segunda Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados3:
              {Indice: '4',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Tercera Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados4:
              {Indice: '5',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Cuarta Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados5:
              {Indice: '6',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Quinta Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados6:
              {Indice: '7',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Sexta Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,
          improvisados7:
              {Indice: '8',Semestre: '1',TBole_Factura:'1',TCodigo: '1',TConcepto: 'Pension: Septima Cuota',TDebe: '0',TFecha_Pago: '1',TFecha_Vencimiento: '1',THaber: '0',TVoucher: '1',nv:0}

          ,

          tablas:[],
          Sem:[
            '16-1','16-2','17-1','17-2','18-1','18-2','19-1','19-2','20-1','20-2','21-1','21-2','22-1','22-2','23-1','23-2','24-1','24-2','25-1','25-2','26-1','26-2'
          ],  
        headers: [
          {
            text: 'Semestre',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Fecha Vencimiento', value: 'calories' , sortable: false  },
          { text: 'Fecha Pago', value: 'fat' , sortable: false },
          { text: 'Voucher', value: 'carbs' , sortable: false },
          { text: 'Boleta/Factura', value: 'protein', sortable: false  },
          { text: 'Concepto', value: 'iron', sortable: false  },
          { text: 'Dias', value: 'iron' , sortable: false },
          { text: 'Debe', value: 'iron' , sortable: false },
          { text: 'Haber', value: 'iron', sortable: false  },
          { text: 'Saldo', value: 'iron' , sortable: false },
          { text: 'Actions', value: 'name', sortable: false }
        ],
         descriptionLimit: 60,
          entries: [],
          isLoading: false,
         

          search: null
        
      }
    },

    methods: {

      
        

        
      exportTableToExcel(tableID,tableID2,tableID3,tableID4,tableID5,tableID6,tableID7,tableID8, filename = ''){
          var downloadLink;
          var dataType = 'application/vnd.ms-excel';
          var tableSelect = document.getElementById(tableID);
          var tableSelect1 = document.getElementById(tableID2);
          var tableSelect2 = document.getElementById(tableID3);
          var tableSelect3 = document.getElementById(tableID4);
          var tableSelect4 = document.getElementById(tableID5);
          var tableSelect5 = document.getElementById(tableID6);
          var tableSelect6= document.getElementById(tableID7);
          var tableSelect7 = document.getElementById(tableID8);
          

        


          // var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
          // var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
          // var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
          // var tableHTML3 = tableSelect3.outerHTML.replace(/ /g, '%20');
          // var tableHTML4 = tableSelect4.outerHTML.replace(/ /g, '%20');
          // var tableHTML5 = tableSelect5.outerHTML.replace(/ /g, '%20');
          // var tableHTML6 = tableSelect6.outerHTML.replace(/ /g, '%20');
          // var tableHTML7 = tableSelect7.outerHTML.replace(/ /g, '%20');
          
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

              if(tableSelect1 == null){
                console.log("quedo en el 1");
                 var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                 // Create a link to the file
                downloadLink.href = 'data:' + dataType + ', ' + tableHTML;
            
                // Setting the file name
                downloadLink.download = filename;
                
                //triggering the function
                downloadLink.click();

              }
              else{
                if(tableSelect2 == null){
                   console.log("quedo en el 2");
                   var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                  var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                   
                  // Create a link to the file
                  downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1;
              
                  // Setting the file name
                  downloadLink.download = filename;
                  
                  //triggering the function
                  downloadLink.click();

                }
                else{
                   if(tableSelect3 == null){
                      console.log("quedo en el 3");
                      var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                     var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                     var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
                       
                      // Create a link to the file
                      downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2;
                  
                      // Setting the file name
                      downloadLink.download = filename;
                      
                      //triggering the function
                      downloadLink.click();

                  }
                  else{
                    if(tableSelect4 == null){
                       console.log("quedo en el 4");
                       var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                     var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                     var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
                      var tableHTML3 = tableSelect3.outerHTML.replace(/ /g, '%20');
                      downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2+tableHTML3;
            
                      // Setting the file name
                      downloadLink.download = filename;
                      
                      //triggering the function
                      downloadLink.click();

                      }
                      else{
                          if(tableSelect5 == null){
                             console.log("quedo en el 5");
                              var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                              var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                              var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
                                var tableHTML3 = tableSelect3.outerHTML.replace(/ /g, '%20');
                             var tableHTML4 = tableSelect4.outerHTML.replace(/ /g, '%20');

                              downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2+tableHTML3+tableHTML4;
            
                            // Setting the file name
                            downloadLink.download = filename;
                            
                            //triggering the function
                            downloadLink.click();

                        }
                        else{
                            if(tableSelect6 == null){
                               console.log("quedo en el 6");
                               var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                              var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                              var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
                                var tableHTML3 = tableSelect3.outerHTML.replace(/ /g, '%20');
                             var tableHTML4 = tableSelect4.outerHTML.replace(/ /g, '%20');
                              var tableHTML5 = tableSelect5.outerHTML.replace(/ /g, '%20');

                                downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2+tableHTML3+tableHTML4+tableHTML5;
            
                                // Setting the file name
                                downloadLink.download = filename;
                                
                                //triggering the function
                                downloadLink.click();

                                }
                                else{
                                    if(tableSelect7 == null){
                                       console.log("quedo en el 7");
                                        var tableHTML  = tableSelect.outerHTML.replace(/ /g, '%20');
                                        var tableHTML1 = tableSelect1.outerHTML.replace(/ /g, '%20');
                                        var tableHTML2 = tableSelect2.outerHTML.replace(/ /g, '%20');
                                          var tableHTML3 = tableSelect3.outerHTML.replace(/ /g, '%20');
                                      var tableHTML4 = tableSelect4.outerHTML.replace(/ /g, '%20');
                                        var tableHTML5 = tableSelect5.outerHTML.replace(/ /g, '%20');
                                      var tableHTML6 = tableSelect6.outerHTML.replace(/ /g, '%20');
                                          downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2+tableHTML3+tableHTML4+tableHTML5+tableHTML6;
            
                                      // Setting the file name
                                      downloadLink.download = filename;
                                      
                                      //triggering the function
                                      downloadLink.click();

                                        }
                                        else{
                                          Console.log("falta 7 mo tablas");
                                          
                                        }
                                }
                            }
                        
                      }
                    
                  }
                  
                }
              }

              // Create a link to the file
              downloadLink.href = 'data:' + dataType + ', ' + tableHTML+tableHTML1+ tableHTML2+tableHTML3+tableHTML4+tableHTML5;
          
              // Setting the file name
              downloadLink.download = filename;
              
              //triggering the function
              downloadLink.click();
          }
        },

      save () {
        this.snack = true
        this.snackColor = 'success'
        this.snackText = 'Data saved'
      },
      cancel () {
        this.snack = true
        this.snackColor = 'error'
        this.snackText = 'Canceled'
      },
      open () {
        this.snack = true
        this.snackColor = 'info'
        this.snackText = 'Dialog opened'
      },
      close () {
        console.log('Dialog closed')
      },
      Insertar_Registro(){
        console.log(this.pos);
        console.log(this.registros);
        if(this.registros[this.pos].historial.length == 0){
            console.log("llenar Matricula para empezar");
            // this.registros[this.pos].historial[0]=this.improvisados;
             Object.assign(this.registros[this.pos].historial, this.improvisados);


          
            

        //     this.$nextTick(() => {
        //       // this.editedItem = Object.assign({}, this.defaultItem);
        //       // this.editedIndex = -1 ;
        //        Object.assign(this.registros[this.pos].historial, this.improvisados);
               
        // })

            console.log(this.registros[this.pos].historial);
            console.log(this.registros[this.pos]);


        }
        else{
            console.log(this.registros[this.pos].historial.length);
         switch ( this.registros[this.pos].historial.length) {
          case 0:
           console.log("Definir Matricula");
            break;
          case 1:
            // console.log(this.someObject);
            // this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })
            // this.registros[2].historial[1] =  Object.assign(this.registros[2].historial[1], this.improvisados1);
            //  this.registros[2].historial[1]=this.improvisados1;
            this.registros[this.pos].historial.push(this.improvisados1);
           
            // Object.assign(this.registros[2].historial, this.improvisados1);
            console.log("Definir Primera Cuota");  
            console.log(this.registros[2].historial);
            break;
        
          case 2:
            console.log("Definir Segunda Cuota");  
            this.registros[this.pos].historial.push(this.improvisados2);
            break;

          case 3:
            console.log("Definir Tercera Cuota");
            this.registros[this.pos].historial.push(this.improvisados3);   
            break; 
          
          case 4:
            console.log("Definir Cuarta Cuota");
            this.registros[this.pos].historial.push(this.improvisados4);   
            break;

          case 5:
            console.log("Definir Quinta Cuota");
            this.registros[this.pos].historial.push(this.improvisados5);   
            break;
            
          case 6:
            console.log("Definir Sexta Cuota");
            this.registros[this.pos].historial.push(this.improvisados6);   
            break;
            
          case 7:
            console.log("Definir Septima Cuota");
            this.registros[this.pos].historial.push(this.improvisados7);   
            break;  

          default:
            console.log("Demasiadas filas");
            break;
        }
        console.log(this.registros[this.pos].historial);
       } 

      },

      Activar_Tabla(){
          if(this.R_1 == true){
                  
              if(this.R_2 == true){
                 if(this.R_3==true){
                   if(this.R_4==true){
                    //  console.log("No hay mas tablas para crear ");
                        if(this.R_5==true){
                    
                            if(this.R_6==true){
                              
                                if(this.R_7==true){
                    
                                  console.log("No hay mas tablas para crear ");
                      
                                }
                                else(this.R_7==false)
                                  Object.assign(this.registros[7].historial, this.improvisados);
                                   this.R_7=true;
                              
                            }
                            else(this.R_6==false)
                              Object.assign(this.registros[6].historial, this.improvisados);
                              this.R_6=true;
                          }
                         else(this.R_5==false) 
                              Object.assign(this.registros[5].historial, this.improvisados);
                              this.R_5=true;
                   }
                   else(this.R_4==false)
                      Object.assign(this.registros[4].historial, this.improvisados);
                          this.R_4=true;
                    
                 }
                 else(this.R_3==false)
                       Object.assign(this.registros[3].historial, this.improvisados); 
                        this.R_3=true;
                      
              }
              else(this.R_2==false)
              
               Object.assign(this.registros[2].historial, this.improvisados);
                        console.log("no te creas tan importante");
                        console.log(this.registros);
              this.R_2=true;
              
          }
          else(this.R_1==false)

            this.R_1=true;
          
      },
      GuardarFila(valor){
        // console.log(this.pos);
        // console.log(this.registros[this.pos].historial[this.valor].nv);
          console.log("aqui el caso ......");
          console.log(this.registros[this.pos].historial[this.valor].nv);
          
        switch (this.registros[this.pos].historial[this.valor].nv){

        case 0:
          this.Codigo=this.Codigo;
          this.Semestre_Seleccionado=this.registros[this.pos].historial[this.valor].Semestre;
          this.date=this.registros[this.pos].historial[this.valor].TFecha_Vencimiento;
          this.datofin=this.registros[this.pos].historial[this.valor].TFecha_Pago;
          this.VOUCHER=this.registros[this.pos].historial[this.valor].TVoucher;
          this.BF=this.registros[this.pos].historial[this.valor].TBole_Factura;
          this.Concepto1=this.registros[this.pos].historial[this.valor].TConcepto;
          this.DEBE=this.registros[this.pos].historial[this.valor].TDebe;
          this.HABER=this.registros[this.pos].historial[this.valor].THaber;

          console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date+'/'+this.datofin+'/'+this.VOUCHER+'/'+this.BF+'/'+this.Concepto1+'/'+this.DEBE+'/'+this.HABER);
          if(this.BF == ''){
              this.BF=this.SError;
          }
          this.Ingresar_Tabla1();
          break; 
        case 1:
          this.Codigo=this.Codigo;
          this.Semestre_Seleccionado=this.registros[this.pos].historial[this.valor].Semestre;
          this.date2=this.registros[this.pos].historial[this.valor].TFecha_Vencimiento;
          this.datofin2=this.registros[this.pos].historial[this.valor].TFecha_Pago;
          this.VOUCHER2=this.registros[this.pos].historial[this.valor].TVoucher;
          this.BF2=this.registros[this.pos].historial[this.valor].TBole_Factura;
          this.Concepto2=this.registros[this.pos].historial[this.valor].TConcepto;
          this.DEBE2=this.registros[this.pos].historial[this.valor].TDebe;
          this.HABER2=this.registros[this.pos].historial[this.valor].THaber;
          
          if(this.BF2 == ''){
              this.BF2=this.SError;
          }
          this.Editar_Tabla();
          break;
        }
        


        console.log("Fila Editada");
      },
      EliminarFila(){
        console.log("Fila Eliminada");
      },
      Mostrar_Registro(){
               axios.get('/apipagos/v1/busca/'+this.Codigo+'/'+this.Concepto, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    // this.historial=response.data;
                    this.Numero_Tabla = response.data;
                    
                    
                    console.log("aqui numero de tablas");
                    console.log(this.Numero_Tabla);
                    console.log("numero de tabla arribita");
                    // console.log(this.Numero_Tabla[1].Semestre);
                    // this.numero=this.Numero_Tabla.length;
                    //  console.log(this.numero);
                    //  console.log(this.contador);
                    // while(this.numero>0){
                    //     this.datos[this.contador].id=this.contador;
                    //     this.contador=this.contador+1;
                    //     console.log(this.contador);
                    //     this.numero=this.numero-1;
                    // }
                    
                        this.Numero_Tabla.forEach(Numero_Tabla=>{
                      this.semestres.push(Numero_Tabla.Semestre);
                      
                      
                      })
                 

                     console.log(this.semestres);
                
                 this.Agregar_Alumno(); 
                  this.Agregar_Alumno2();
                  this.Agregar_Alumno3();
                  this.Agregar_Alumno4();
                  this.Agregar_Alumno5();






                })
                .catch(function (error) {
                    
                    console.log(error);
                });
          

      },
      Mostrar_Registros_Tablas(){
        console.log(this.R_1+'+'+this.R_2+'+'+this.R_3+'+'+this.R_4);
        this.modelC=true;
        this.Mostrar_Registro();
        
      },
      Boton_GI(){
        
        switch (this.Controlador) {

        case 1 :
          break;
        case 2:
          break;
          
          }
      },
      GuardarDato1(){
        console.log("Aqui los registros");
        this.Codigo=this.registros[0].historial[0].TCodigo;
        this.Semestre_Seleccionado=this.registros[0].historial[0].Semestre;
        this.date=this.registros[0].historial[0].TFecha_Vencimiento;
        this.datofin=this.registros[0].historial[0].TFecha_Pago;
        this.VOUCHER=this.registros[0].historial[0].TVoucher;
        this.BF=this.registros[0].historial[0].TBole_Factura;
        this.Concepto1=this.registros[0].historial[0].TConcepto;
        this.DEBE=this.registros[0].historial[0].TDebe;
        this.HABER=this.registros[0].historial[0].THaber;
        this.Ingresar_Tabla1();
        console.log(this.registros[0].historial[0].Indice);
 
      }, 
      EditarFila(n){
        console.log(this.registros[1]);
        this.Codigo=this.registros[1].historial[n].TCodigo;
        this.Semestre_Seleccionado=this.registros[1].historial[n].Semestre;
        this.date=this.registros[1].historial[n].TFecha_Vencimiento;
        this.datofin=this.registros[1].historial[n].TFecha_Pago;
        this.VOUCHER=this.registros[1].historial[n].TVoucher;
        this.BF=this.registros[1].historial[n].TBole_Factura;
        this.Concepto1=this.registros[1].historial[n].TConcepto;
        this.DEBE=this.registros[1].historial[n].TDebe;
        this.HABER=this.registros[1].historial[n].THaber;
        console.log(this.HABER);

      },
      Ingresar_Datos(){
        this.Ingresar_Tabla1();
        this.Ingresar_Tabla2();
        this.Ingresar_Tabla3();
        this.Ingresar_Tabla4();
        this.Ingresar_Tabla5();
      },
      Editar_Tabla(){
        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date2+'/'+this.datofin2+'/'+this.VOUCHER2+'/'+this.BF2+'/'+this.Concepto2+'/'+this.DEBE2+'/'+this.HABER2);
         axios.get('/apipagos/v1/registro2/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date2+'/'+this.datofin2+'/'+this.VOUCHER2+'/'+this.BF2+'/'+this.Concepto2+'/'+this.DEBE2+'/'+this.HABER2,
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    console.log("datos modificados");
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Ingresar_Tabla1(){

        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date+'/'+this.datofin+'/'+this.VOUCHER+'/'+this.BF+'/'+this.Concepto1+'/'+this.DEBE+'/'+this.HABER);
        axios.get('/apipagos/v1/registro1/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date+'/'+this.datofin+'/'+this.VOUCHER+'/'+this.BF+'/'+this.Concepto1+'/'+this.DEBE+'/'+this.HABER, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    console.log("datos encviados");
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Ingresar_Tabla2(){
        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date2+'/'+this.datofin2+'/'+this.VOUCHER2+'/'+this.BF2+'/'+this.Concepto2+'/'+this.DEBE2+'/'+this.HABER2);
        axios.get('/apipagos/v1/registro1/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date2+'/'+this.datofin2+'/'+this.VOUCHER2+'/'+this.BF2+'/'+this.Concepto2+'/'+this.DEBE2+'/'+this.HABER2, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
    
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Ingresar_Tabla3(){
        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date3+'/'+this.datofin3+'/'+this.VOUCHER3+'/'+this.BF3+'/'+this.Concepto3+'/'+this.DEBE3+'/'+this.HABER3);
        axios.get('/apipagos/v1/registro1/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date3+'/'+this.datofin3+'/'+this.VOUCHER3+'/'+this.BF3+'/'+this.Concepto3+'/'+this.DEBE3+'/'+this.HABER3, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
    
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Ingresar_Tabla4(){
        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date4+'/'+this.datofin4+'/'+this.VOUCHER4+'/'+this.BF4+'/'+this.Concepto4+'/'+this.DEBE4+'/'+this.HABER4);
        axios.get('/apipagos/v1/registro1/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date4+'/'+this.datofin4+'/'+this.VOUCHER4+'/'+this.BF4+'/'+this.Concepto4+'/'+this.DEBE4+'/'+this.HABER4, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
    
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Ingresar_Tabla5(){
        console.log(this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date5+'/'+this.datofin5+'/'+this.VOUCHER5+'/'+this.BF5+'/'+this.Concepto5+'/'+this.DEBE5+'/'+this.HABER5);
        axios.get('/apipagos/v1/registro1/'+this.Codigo+'/'+this.Semestre_Seleccionado+'/'+this.date5+'/'+this.datofin5+'/'+this.VOUCHER5+'/'+this.BF5+'/'+this.Concepto5+'/'+this.DEBE5+'/'+this.HABER5, 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
    
                })
                .catch(function (error) {
                  console.log(error);
                });
      },
      Mostrar_Datos(){
          this.model=true;
          console.log(this.Codigo);
          axios.get("/apipagos/v1/internos/"+this.Codigo,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                
                 this.cadena_Alumno = response.data;
                //  console.log(this.cadena_Alumno);
                  this.DNI=this.cadena_Alumno[0].DNI;
                  this.CODIGO=this.cadena_Alumno[0].Codigo;
                  this.COD_ESP=this.cadena_Alumno[0].Esp;
                  this.MAESTRIA=this.cadena_Alumno[0].Maestria;
                  this.NOMBRES_APELLIDOS=this.cadena_Alumno[0].Alumno;
        
                 
                
               
            })
      },
      Traer_Codigos(){
          axios.get("/apipagos/v1/internos/"+this.Cero,
            {headers: { 'content-type': 'application/form-data' }})
            .then(response => {
                
                 this.cadena_codigos = response.data;
                 console.log(this.cadena_codigos);
                 this.cadena_codigos.forEach(cadena_codigos=>{
                this.Codigos.push(cadena_codigos.DNI);
                
                
                 })
                
               
            })
      },
      LLenar_Datos(){
            this.items.name='MARCOS';
            // this.calories.fecha='setiembre';
            // this.calories.pago='210';
            this.fat= 'fat';
            this.carbs= 'tu';
            this.protein= 'ta';
            this.sodium= 'dura';
            this.calcium= 'sin';
            this.iron= 'ir al gym';

      },
      Ver(){
        console.log("Activando boton Verd");
      },

      Agregar_Alumno(){
        console.log(this.semestres[0]);
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[0], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    // this.historial=response.data;
                    this.registros[0].historial = response.data;
                    if(this.registros[0].historial.length !== 0){
                    this.R_0=true;
                    console.log(this.k);
                    for( this.k ; this.k <this.registros[0].historial.length;this.k++ ){
                        this.registros[0].historial[this.k].nv=1;
                    }
                    console.log("Conteo de Registros primera tabla :"+this.registros[0].historial.length);
                    console.log(this.registros[0].historial[0].THaber);
                    // console.log("registroooossss"+this.registros);
                    }
                   
                    
                    
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                });
            
             
             
              
          },
           Agregar_Alumno2(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[1], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[1].historial = response.data;
                    if(this.registros[1].historial.length !== 0){
                    this.R_1=true;
                    for( this.x ; this.x <this.registros[1].historial.length;this.x++ ){
                        this.registros[1].historial[this.x].nv=1;
                    }
                    console.log("Conteo de Registros Segunda  tabla :"+this.registros[1].historial.length);
                    }  
                    
                    
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                });
            
             
             
              
          },
          Agregar_Alumno3(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[2], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[2].historial = response.data;
                    if(this.registros[2].historial.length !== 0){
                    this.R_2=true;
                    for( this.y ; this.y <this.registros[2].historial.length;this.y++ ){
                        this.registros[2].historial[this.y].nv=1;
                    }
                    console.log("Conteo de Registros tercera tabla :"+this.registros[2].historial.length);
                    }
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                });
            
             
             
              
          }, 
          Agregar_Alumno4(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[3], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[3].historial = response.data;
                    if(this.registros[3].historial.length !== 0){
                    this.R_3=true;
                    for( this.w ; this.w <this.registros[3].historial.length;this.w++ ){
                        this.registros[3].historial[this.w].nv=1;
                    }
                    console.log("Conteo de Registros cuarta tabla :"+this.registros[3].historial.length);

                    }
                    
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros[3].historial);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                    console.log("Sin datos agregar_alumno4");
                });
            
             
             
              
          },
          Agregar_Alumno5(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[4], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[4].historial = response.data;
                    if(this.registros[4].historial.length !== 0){
                    this.R_4=true;
                    for( this.z ; this.z <this.registros[4].historial.length;this.z++ ){
                        this.registros[4].historial[this.z].nv=1;
                    }
                    console.log("Conteo de Registros QUINTA tabla :"+this.registros[4].historial.length);

                    }
                    
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros[4].historial);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                    console.log("Sin datos agregar_alumno4");
                });
            
          },
          Agregar_Alumno6(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[5], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[5].historial = response.data;
                    if(this.registros[5].historial.length !== 0){
                    this.R_5=true;
                    for( this.a1 ; this.a1 <this.registros[5].historial.length;this.a1++ ){
                        this.registros[5].historial[this.a1].nv=1;
                    }
                    console.log("Conteo de Registros QUINTA tabla :"+this.registros[5].historial.length);

                    }
                    
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros[5].historial);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                    console.log("Sin datos agregar_alumno4");
                });
            
             
             
              
          },  
          Agregar_Alumno7(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[6], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[6].historial = response.data;
                    if(this.registros[6].historial.length !== 0){
                    this.R_6=true;
                    for( this.a2 ; this.a2 <this.registros[6].historial.length;this.a2++ ){
                        this.registros[6].historial[this.a2].nv=1;
                    }
                    console.log("Conteo de Registros QUINTA tabla :"+this.registros[6].historial.length);

                    }
                    
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros[6].historial);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                    console.log("Sin datos agregar_alumno4");
                });
            
             
             
              
          },  
          Agregar_Alumno8(){
             axios.get('/apipagos/v1/tabla/' +this.Codigo+'/'+this.semestres[7], 
                {
                },
                { headers: {
                    'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
                }
                })
                .then((response) => {
                    this.registros[7].historial = response.data;
                    if(this.registros[7].historial.length !== 0){
                    this.R_7=true;
                    for( this.a3 ; this.a3 <this.registros[7].historial.length;this.a3++ ){
                        this.registros[7].historial[this.a3].nv=1;
                    }
                    console.log("Conteo de Registros QUINTA tabla :"+this.registros[7].historial.length);

                    }
                    
                    console.log("AQUI LOS REGISTROS-----------");
                    console.log(this.registros[7].historial);
                    // eslint-disable-next-line
                    //console.log(response);
                    
                    // this.Codig='';
                    
                })
                .catch(function (error) {
                    // eslint-disable-next-line
                    console.log(error);
                    console.log("Sin datos agregar_alumno4");
                });
            
             
             
              
          },  
                    
    },
    created() {
      
      this.Traer_Codigos();
          
    },
    computed:{

      



         fields () {
        if (!this.model) return []

        return Object.keys(this.model).map(key => {
          return {
            key,
            value: this.model[key] || 'n/a'
          }
        })
      },
      items () {
        return this.entries.map(entry => {
          const Description = entry.Description.length > this.descriptionLimit
            ? entry.Description.slice(0, this.descriptionLimit) + '...'
            : entry.Description

          return Object.assign({}, entry, { Description })
        })
      }
    },
    watch:{
      
      
      loader () {
        const l = this.loader
        this[l] = !this[l]

        setTimeout(() => (this[l] = false), 3000)

        this.loader = null
      },
      
       search (val) {
        // Items have already been loaded
        if (this.items.length > 0) return

        // Items have already been requested
        if (this.isLoading) return

        this.isLoading = true

        // Lazily load input items
       
        
        fetch('https://api.publicapis.org/entries')
          .then(res => res.json())
          .then(res => {
            const { count, entries } = res
            this.count = count
            this.entries = entries
          })
          .catch(err => {
            console.log(err)
          })
          .finally(() => (this.isLoading = false))
      }
    }
    }
  
</script>

<style >
.v-table__overflow {
    width: 100%;
    overflow-x: auto;
    overflow-y: auto;
    height: 360px !important;
    /* width: 992px; */
}
  .custom-loader {
    animation: loader 1s infinite;
    display: flex;
  }
  @-moz-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-webkit-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-o-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  .step1 {
  background: linear-gradient(to right, #f12711, #f5af19);
  padding: 0 40px;
}
</style>