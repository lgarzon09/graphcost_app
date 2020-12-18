<template>
  <div class="card_login">

    <div style="width: 47%">
      <img src="../assets/imageLogin.jpg" id="imageLogin">
    </div>

    <div style="width: 52%">
      
      <b-container fluid id="container_login">

        <b-row class="justificCenter">
          <h1 style="font-weight: bolder;"><bold>GraphCost</bold></h1>
          <h6>El mejor aliado para el manejo de tu código</h6>
        </b-row>

        <b-form @submit.prevent="login">
                  
          <b-row style="margin-top:50px">
            <b-col class="justificCenter">
              <b-button id="btn_admin">Administrador</b-button>
            </b-col>
            <b-col class="justificCenter">
              <b-button id="btn_recep">Recepcionista</b-button>
            </b-col>
          </b-row>

          <b-row class="displayColumn" style="margin-top:23px">
            <b-col style="margin-bottom: 15px;">
              <b-form-input type="email" placeholder="Correo electrónico" id="email" required v-model="form.email"></b-form-input>
            </b-col>
            <b-col>
              <b-form-input type="password" placeholder="Contraseña" id="password" required v-model="form.password"></b-form-input>
            </b-col>
          </b-row>

          <b-row class="justificCenter">
            <p v-if="error" style="color: red">Email y/o contraseña incorrectos</p>
            <b-button id="btn_login" type="submit">Iniciar sesión</b-button>
          </b-row>
        </b-form>        
        
        <b-row class="justificCenter" style="margin-top:10px">
          <p>No tienes una cuenta? <b-button v-b-modal.modal-1 id="btn_register">Regístrate aquí</b-button></p>
        </b-row>
        
      </b-container>
      
    </div>

    <b-modal id="modal-1" size="xl" title="BootstrapVue">
      
    </b-modal>
      
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      form:{
        email: '',
        password: '',
        selected: '',
        error: false
      }
    }
  }
}
</script>

<style scoped>
  .card_login{
    width: 70%;
    margin: auto;
    margin-top: 50px;
    border-radius: 15px;
    background-color: white;
    display: flex; flex-direction: row;
    box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  }

  #imageLogin{
    width:90%;
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
  }

  #btn_admin{
    padding-top: 6px;
    padding-bottom: 6px;
    width: 100%;
    border-radius: 5px;
    background-color: #0c4c03;
  }

  #btn_recep{
    padding-top: 6px;
    padding-bottom: 6px;
    width: 100%;
    border-radius: 5px;
    border-color: #0c4c03;
    border-width:2px;
    background-color: white;
    color: #0c4c03;
  }
  
  #btn_login{
    color: white;
    border-radius: 20px;
    width: 50%;
    background-color: #0c4c03;
    margin-top: 60px;
    box-shadow: 0 10px 13px -2px #ced6e0;
  }
  
  #btn_register{
    padding:0;
    color: blue;
    background-color: none;
    border: none;
    ;
  }

  .justificCenter{
    display:flex; 
    justify-content: center
  }

  .displayColumn{
    display:flex; 
    flex-direction: column
  }

  #container_login{
    padding-right: 80px; 
    margin-top: 60px;
  }


</style>
