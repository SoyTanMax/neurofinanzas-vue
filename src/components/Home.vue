<template>
  <div class="home">
    <div class="hero" :style="{'background-image':'linear-gradient(rgba(245, 246, 252, 0.2), rgba(34, 235, 141, 0.75)), url(https://bit.ly/2YCMp7L)'}">
      <div class="hero-header">
        <Navbar/>
      </div>
      <div class="container">
        <div class="encabezado is-size-1 has-text-weight-bold is-pulled-left has-text-white">{{ title }}</div>
        <button class="button galeria is-rounded is-uppercase">
          <i class="fas fa-play"></i> Galería
        </button>
      </div>
    </div>
    <div class="box">
      <div class="boxTitle is-size-2 has-text-weight-bold has-text-centered is-uppercase">{{ boxTitle }}</div>
      <div class="proposito is-size-4 has-text-weight-bold has-text-centered">{{ proposito }}</div>
      <div class="descripcion is-size-5 has-text-centered">{{ descripcion }}</div>
        <div class="columns">
          <div v-for="(elemento, index) in elementos" class="column" :key="index">
            <img class="image" :src="elemento.image"/>
            <p class="elementoTitle has-text-centered">{{ elemento.titulo }}</p>
            <p class="elementoDesc has-text-centered">{{ elemento.desc }}</p> 
            <div class="column buttonContainer">
              <button class="button ver has-text-white is-uppercase is-rounded has-text-weight-medium">ver más</button>
            </div>
          </div>
        </div>
    </div>
    <div class="section is-small">
      <p class="sectionTitle is-size-2 has-text-centered">Alianzas</p>
      <div class="columns is-multiline">
        <div v-for="(alianza, index) in alianzas" :key="index" class="column is-one-third is-vcentered alianza">
          <img class='imageAlianza' :src="alianza.image"/>
          <p class="has-text-centered is-size-5 alianzaTitle">{{ alianza.titulo }}</p>    
        </div>
      </div>
    </div>
    <div class="section is-small greySection">
      <div class='teamContainer'>
        <p class="has-text-centered sectionTitle is-size-2">Conoce al equipo</p>
        <div class="columns is-multiline">
          <div v-for="(miembro, index) in miembros" class="column is-one-fifth alianza" :key="index">
            <img class="imageMiembro" :src="miembro.image"/>
            <p class="is-size-5 has-text-centered">{{ miembro.nombre }}</p>
            <p class="is-size-6 has-text-centered">{{ miembro.puesto }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="section is-small greySection">
      <p class="has-text-centered sectionTitle is-size-2">¡Únete al equipo de Neurofinanzas!</p>
      <p class="has-text-centered descripcion is-size-5">{{ form }}</p>
      <form @submit.prevent="send">
        <div class="forms">
          <div class="columns">
            <div class="column">
              <div class="field">
                <div class="label">Nombre completo</div>
                <div class="control has-icons-left">
                  <validation-provider rules="required" v-slot="{ errors }">
                    <input type="text" name="name" class="input" placeholder="Nombre completo">
                    <span class="icon is-small is-left">
                      <i class="material-icons">person</i>
                    </span>
                    <span class="help is-danger">{{ errors[0] }}</span>
                  </validation-provider>
                </div>
              </div>
              <div class="field">
                <div class="label">Correo electrónico</div>
                <div class="control has-icons-left">
                  <validation-provider rules="required|email" v-slot="{ errors }">
                    <input type="email" name="email" class="input" placeholder="ejemplo@gmail.com">
                    <span class="icon is-small is-left">
                        <i class="material-icons">email</i>
                    </span>
                    <span class="help is-danger">{{ errors[0] }}</span>
                  </validation-provider>
                </div>
              </div>
            </div>
            <div class="column">
              <div class="field">
                <div class="label">Por qué te gustaría ser parte del equipo de Neurofinanzas?</div>
                <input type="message" name="message" class="input msg" placeholder="">
              </div>
              <div class="enviar-button">
                <button class="button has-text-weight-medium has-text-green is-pulled-right has-text-white enviar-button">Enviar</button>
              </div>
            </div>  
          </div>  
        </div> 
      </form>
    </div>
  </div>
</template>

<script>
  import Navbar from '@/components/Navbar'
  import { ValidationProvider, extend } from 'vee-validate';
  import { required, email, min} from 'vee-validate/dist/rules';

  extend('email', email)

  extend('required', {
  ...required,
  message: 'Este campo es requerido'
  });

  export default {
    name: 'Home',
    components: {
      Navbar,
      ValidationProvider
    },
    data () {
      return {
        title: 'Empieza a cambiar tu historia con Neurofinanzas',
        boxTitle: 'Nuestro propósito',
        proposito: 'Construir prosperidad social de persona en persona, de familia en familia.',
        descripcion: 'Somos una Asociación Civil cuya oferta promueve un modelo disruptivo de Educación Financiera.',
        elementos: [
          { titulo: 'Foro de Neurofinanzas', desc: 'Cada tercer miércoles de mes, charlamos sobre finanzas en un espacio incluyente y libre de ventas. ¡Toda la familia es bienvenida!', image: require('@/assets/foro.svg')},
          { titulo: 'Educación Financiera para empresas', desc: 'Tenemos una metodología con programas registrados ante la STPS para que el dinero deje de ser un factor de estrés para el personal de tu empresa.', image: require('@/assets/educacion.svg')},
          { titulo: 'Taller "Dinero a tu favor"', desc: 'Taller de 8 sesiones, para cambiar la forma en que te relacionas con el dinero y tomar mejores desiciones financieras para una vida próspera.', image: require('@/assets/taller.svg')}
        ],
        alianzas:[
          {titulo: 'Tec de Monterrey', image: require('@/assets/tec.png')},
          {titulo: 'Inmoviliaria Lux', image: require('@/assets/lux.png')},
          {titulo: 'Zonga', image: require('@/assets/zonga.png')},
          {titulo: 'Embajada de USA en México', image: require('@/assets/embajada.png')},
          {titulo: 'Secretaría de Economía de N.L.', image: require('@/assets/secretaria.png')},
          {titulo: 'UDEM', image: require('@/assets/udem.png')},
          {titulo: 'Marketplace Literacy Project', image: require('@/assets/mlp.png')},
          {titulo: 'Ticketopolis', image: require('@/assets/ticket.svg')},
          {titulo: 'Fotophy', image: require('@/assets/fotophy.svg')}
        ],
        miembros:[
          {nombre: 'Cristina', puesto: 'Fundadora', image: require('@/assets/cristina.png')},
          {nombre: 'Alejandra', puesto: 'Logística', image: require('@/assets/alejandra.png')},
          {nombre: 'Yolanda', puesto: 'Talento Creativo', image: require('@/assets/yolanda.png')},
          {nombre: 'Fernando', puesto: 'Logística', image: require('@/assets/fernando.png')},
          {nombre: 'Blanca', puesto: 'Logística', image: require('@/assets/blanca.png')},
          {nombre: 'Angela', puesto: 'Talento Creativo', image: require('@/assets/angela.png')},
          {nombre: 'Ricardo', puesto: 'Organizador', image: require('@/assets/ricardo.png')},
          {nombre: 'Concepción', puesto: 'Servicio Social', image: require('@/assets/concepcion.png')},
          {nombre: 'Priscilia', puesto: 'Logística', image: require('@/assets/priscilia.png')},
          {nombre: 'Lydia', puesto: 'Sistematización', image: require('@/assets/lydia.png')}
        ],
        form:'Ayuda a más personas a educarse para lograr la autonomía financiera y aprende mucho en la marcha. ¡Genera relaciones a largo plazo, y construye patrimonio propio! ¡JUNTOS ES POSIBLE!'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  @import url('https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@100;500;700&display=swap');

  .hero{
  
    background-size: cover;
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    height: 640px;
  }
  .container{
    width: 384px;
    margin: 96px 96px;
  }
  .encabezado{
    line-height: 1.2;
    font-family: 'Roboto Slab', serif;
  }
  .galeria{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
    width: 156px;
    height: 64px;
    color: #35A849;
    background-color: white;
    border-color: white;
    margin-top: 24px;
    align-items: center;
  }
  .fa-play{
    margin-right: 8px;
  }
  .box{
    width: 90%;
    margin: -48px auto 0;
    height: 100%;
  }
  .boxTitle{
    margin-top: 48px;
    color: #35A849; 
    font-family: 'Roboto Slab', serif;
  }
  .proposito{
    width: 65%;
    margin: 32px auto 16px;
    font-family: Arial, Helvetica, sans-serif;
    color: rgb(141, 140, 140);
  }
  .descripcion{
    width: 70%;
    margin: 0 auto 24px;
    font-family: Arial, Helvetica, sans-serif;
    color: rgb(141, 140, 140);
  }
  .image{
    margin: 0 auto;
  }
  .elementoTitle{
    color: #35A849;
    font-family: 'Roboto Slab', serif;
    font-weight: 700;
    font-size: 18px;
    margin-top: 12px;
    margin-bottom: 24px;
  }
  .elementoDesc{
    color: rgb(141, 140, 140);
  }
  .ver{
    background-color: #35A849;
    width: 128px;
    height: 48px;
    font-size: 14px;
  }
  .buttonContainer{
    display: flex;
    justify-content: center;
    align-content: flex-end;
  }
  .alianza{
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
  }
  .imageAlianza{
    max-width: 128px;
  }
  .alianzaTitle{
    font-family: 'Roboto Slab', serif;
    padding: 16px 0;
  }
  .greySection{
    background-color: #f9f9f9;
  }
  .imageMiembro{
    max-width: 96px;
  }
  .sectionTitle{
    color: #35A849;
    font-family: 'Roboto Slab', serif;
    font-weight: 700;
    margin: 24px 0;
  }
  .teamContainer{
    margin: 0 64px;
  }
  .forms{
    margin: 0 96px;
  }
  .msg{
    height: 128px;
  }
  .enviar-button{
    margin: 12px 0;
    background-color: #35A849;
    border: none;
  }
  .label{
    color:rgb(114, 112, 112);
  }

</style>
