<script >
export default{
  props: ["Messages"],
};
</script>

<template> 
  <!-- Ventana Chat --> 
  <div class="overflow-y-scroll d-flex flex-column mx-3  rounded-2 p-4 bg-body-secondary  border border-3" id="Chat">
    <!-- Contenedor mensaje -->
      <div v-for="(Message, index) in Messages" :key="index"     
        class="my-2 "
        :class="{user1: Message.id == 1, user2: Message.id == 2,}">
        <!-- Nombre Usuario -->
          <p class="fs-6 fw-normal mb-0" >{{Message.userName}} </p>
          <!-- Globo de texto -->
          <div class="p-2 rounded-4" :style="{backgroundColor: Message.color, }">
            <!-- Texto mensaje -->
            <p class="m-0 p-1 text-start" >{{Message.mssg}}</p>
          </div>        
       </div>   
  </div>   
</template>

<style scoped>

#Chat{
  width: 30rem;
  height: 30rem; 
}

.user1{ 
  align-self: flex-start;
  text-align:left;  
}

.user2{
  align-self: flex-end;  
  text-align:right;
}

</style>
