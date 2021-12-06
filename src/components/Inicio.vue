<template>
<div>
<div>
  <v-carousel>
    <v-carousel-item 
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
    ></v-carousel-item>
  </v-carousel>
  </div>
  <div>
    <v-item-group>
    <v-container grid-list-md>
      <v-layout wrap>
        <v-flex
         
          xs12
          md4
        >
          <v-item>
            <v-card 

              style="background-color: #09c4e2;"
              slot-scope="{ active, toggle }"
              :color="active ? 'primary' : ''"
              class="d-flex align-center"
              dark
              height="200"
              @click="Enviar_Tablas"
            >
              <v-scroll-y-transition>
                <div
                  
                  class="display-3 text-xs-center"
                >
                  AGREGAR ALUMNO
                </div>
              </v-scroll-y-transition>
            </v-card>
          </v-item>
        </v-flex>
        <v-flex
          
          xs12
          md4
        >
          <v-item>
            <v-card style="background-color: #21da62;"
              slot-scope="{ active, toggle }"
              :color="active ? 'primary' : ''"
              class="d-flex align-center"
              dark
              height="200"
              @click="Enviar_Insertar"
            >
              <v-scroll-y-transition>
                <div
                 
                  class="display-3 text-xs-center"
                >
                  REGISTRO DE PAGO
                </div>
              </v-scroll-y-transition>
            </v-card>
          </v-item>
        </v-flex>
        <v-flex
          
          xs12
          md4
        >
          <v-item>
            <v-card style="background-color: #f7980b;"
              slot-scope="{ active, toggle }"
              :color="active ? 'primary' : ''"
              class="d-flex align-center"
              dark
              height="200"
              @click="Enviar_Reporte"
            >
              <v-scroll-y-transition>
                <div
                 
                  class="display-3 text-xs-center"
                >
                  REPORTE DE PAGO
                </div>
              </v-scroll-y-transition>
            </v-card>
          </v-item>
        </v-flex>
      </v-layout>
    </v-container>
  </v-item-group>
  </div>
  <div>
   <v-footer
    dark
    height="auto"
  >
    <v-card
      flat
      tile
      class="indigo lighten-1 white--text text-xs-center"
    >
      <v-card-text>
        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-3 white--text"
          icon
        >
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
      </v-card-text>

      <v-card-text class="white--text pt-0">
          Los sistemas de pago pueden funcionar bajo esquemas físicos o electrónicos aunque todos los estándares modernos tienden al electrónico. Cada uno tiene sus propias normas, procedimientos y protocolos que suelen estar bajo supervisión del banco central o una institución nacional. 
      </v-card-text>

      <v-divider></v-divider>

      <v-card-text class="white--text">
        &copy;2021 — <strong>FACULTAD CIENCIAS CONTABLES</strong>
      </v-card-text>
    </v-card>
  </v-footer>
  </div>
  </div>
</template>

<script>
import Tablas from '@/components/Tablas';
import Insertar from '@/components/Insertar';
import Reloj from '@/components/Reloj';
  export default {
    
    components: {
      Tablas,Insertar,Reloj
    },
    data () {
      return {
        icons: [
        'fab fa-facebook',
        'fab fa-twitter',
        'fab fa-google-plus',
        'fab fa-linkedin',
        'fab fa-instagram'
      ],
        items: [
          {
            src: 'https://aprendelibvrefiles.blob.core.windows.net/aprendelibvre-container/course/como_usar_windows_10/image/wcuenta_xl.png'
          },
          {
            src: 'https://lh3.googleusercontent.com/proxy/d-AkQoCphSCV9kh-de6N0FsLrGTMQ7DVP6hxr-ybQTT0x-6lfNABAaSkiqJPSiGLcDtFbQnj9-aPIpr8su_3nZ02-UfSkrQN7roCefOJV9i7WEdyxxr-q8Y'
          },
          {
            src: 'https://image.freepik.com/vector-gratis/diseno-fondo-reporte_1300-8.jpg'
          },
          {
            src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg'
          }
        ]
      }
    },
    methods: {
      Enviar_Tablas(){
          this.$router.push('Tablas') ;
    },
    Enviar_Insertar(){
      
          this.$router.push('Insertar') ;

    },
    Enviar_Reporte()
    {
        this.$router.push('Reloj') ;
    }
  
  }
}
</script>
<style>



</style>
