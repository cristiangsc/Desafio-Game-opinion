<template>
  <div class="container mt-4">
    <header>
      <h1>Editando la opinión de: <span class="display-5">{{ comments[payload.id].game }}</span></h1>
    </header>
    <form>
      <label class="fw-bold mb-2">Nombre:</label>
      <input required type="text" v-model="payload.user" class="form-control" :placeholder="comments[payload.id].user">

      <label class="fw-bold mb-2 mt-3">Opiniones:</label>
      <textarea required type="text" v-model="payload.opinion" class="form-control"
                :placeholder="comments[payload.id].opinion"></textarea>
      <br>
      <router-link :to="{name: 'administracion'}">
        <button class="btn btn-primary mx-3">Regresar</button>
      </router-link>
      <button class="btn btn-info mx-3 text-white" @click="editar()">Guardar</button>
    </form>
  </div>
</template>
<script>
import {mapState, mapActions} from 'vuex'

export default {
  data() {
    return {
      payload: {
        user: '',
        opinion: '',
        id: this.$route.params.id,
      }
    };
  },
  computed: {
    ...mapState({
      comments: (state) => {
        return state.comments
      }
    })
  },
  methods: {
    ...mapActions(['editarComentario']),
    editar() {
      if (this.payload.user !== '' || this.payload.opinion !== '') {
        this.editarComentario(this.payload)
        this.$alert("Su comentario ha sido editado con éxito");
      }
    }
  },

}
</script>