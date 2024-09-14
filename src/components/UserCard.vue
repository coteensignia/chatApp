<script>
export default {
  name: 'UserCard',
  data() {
    return {
      message: '',
      color: '' // Inicialmente vacío
    }
  },
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    // Genera un color aleatorio en formato hexadecimal
    generarColorAleatorio() {
      const letters = '0123456789ABCDEF';
      let color = '#';
      for (let i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    },
    enviarMensaje() {
      this.$emit('enviar-mensaje', this.message, this.color, this.user.name.first, this.user.side);
      this.message = '';
    }
  },
  mounted() {
    // Asignamos un color aleatorio cuando el componente se monta
    this.color = this.generarColorAleatorio();
  },
  emits: ['enviar-mensaje']
}
</script>

<template>
  <div class="user-component">
    <h3 style="text-align: center; color:#007bff;">Usuario</h3>
    <div class="card" style="width: 18rem">
      <img :src="user.picture.large" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">{{ user.name.first }} {{ user.name.last }}</h5>

        <!-- Envío de mensaje -->
        <form @submit.prevent="enviarMensaje">
          <!-- El input de color toma el valor del color aleatorio generado -->
          <input v-model="color" type="color" />
          <textarea class="fixed-textarea" v-model="message" placeholder="Escribe tu mensaje"></textarea>
          <div class="d-flex justify-content-end">
            <button class="btn btn-success">Enviar</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fixed-textarea {
  resize: none; 
  overflow: hidden; 
}

form input, form button, textarea {
  width: 100%;
  box-sizing: border-box;
  margin-top: 30px;
}


</style>
