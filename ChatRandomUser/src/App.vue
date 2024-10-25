<script >
import axios from "axios";
import Chat from './components/Chat.vue'

export default{
  name: 'App',
  data(){
     return{  
      Messages: [], 

      user1: {
        id: "1",
        userName: "",
        avatar: "",
        mssg: "",
        color:"#42F236",
      },
      user2: {
        id: "2",
        userName: "",
        avatar: "",
        mssg: "",
        color:"#806AEC",
      },         
     };
  },

  components: {
    Chat,
  },
 
  async mounted () { //Trae los datos de los usuario al cargar la página 
     const url = "https://randomuser.me/api/?results=2";
     const {data} = await axios.get(url);
     
     this.user1.userName = data.results[0].name.first + " " + data.results[0].name.last;
     this.user1.avatar = data.results[0].picture.large; 
     
     this.user2.userName = data.results[1].name.first + " " + data.results[1].name.last;
     this.user2.avatar = data.results[1].picture.large;      
  },

  methods: { 
    sendMessage(user) {  
      // Agrega los usuarios al arreglo Messages   
      this.Messages.push({...user}); 
      // Limpia los campos
      this.user1.mssg = "";
      this.user2.mssg = "";
    },      
  },
};
</script>

<template>
  <div class="contenedor d-flex pb-3 ">
      <!-- Contenedor usuario 1-->
      <div class="d-flex flex-column  border p-4 rounded-5 shadow" >
        <!-- Imagen usuario 1 -->
          <img :src="user1.avatar" class="rounded-4 mb-2" alt="usuario 1"> 
           <!-- Nombre usuario 1 -->     
          <p class="my-1 fs-5">{{ user1.userName }}</p>
           <!-- Selector de color usuario 1 -->
          <input type="color" name="inputUsuario1"  class="col-12 my-2 rounded-3 mb-2" v-model="user1.color">
           <!-- Caja de texto usuario 1 -->
          <textarea rows="5" name="usuario1" id="usuario1" v-model="user1.mssg"></textarea>
          <!-- Boton enviar usuario 1 -->
          <button @click="sendMessage(user1)" class="btn btn-dark mt-3">Enviar</button>
      </div> 

      <!-- Componente hijo -->
      <Chat :Messages />  

      <!-- Contenedor usuario 2-->
      <div class="d-flex flex-column border p-4 rounded-5 shadow" >
         <!-- Imagen usuario 2 -->
          <img :src="user2.avatar" class="rounded-4 mb-2" alt="usuario 2">      
           <!-- Nombre usuario 2 -->
          <p class="my-1 fs-5">{{ user2.userName }}</p>
           <!-- Selector de color usuario 2 -->
          <input type="color" name="inputUsuario2" class="col-12 my-2 rounded-3 mb-2" v-model="user2.color">
           <!-- Caja de texto usuario 2 -->
          <textarea rows="5" name="usuario2" id="usuario2" v-model="user2.mssg"></textarea>
           <!-- Boton enviar usuario 2 -->
          <button @click="sendMessage(user2)" class="btn btn-dark mt-3">Enviar</button>
      </div>
  </div>  
</template>

<style scoped>

</style>
