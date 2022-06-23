<template>
  <div class="container">
    <section v-if="comments.length === 0">
      <svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
        <symbol id="exclamation-triangle-fill" fill="currentColor" viewBox="0 0 16 16">
          <path
              d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
        </symbol>
      </svg>
      <div class="alert alert-danger d-flex align-items-center" role="alert">
        <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Danger:">
          <use xlink:href="#exclamation-triangle-fill"/>
        </svg>
        <div class="fw-bold">
          No existen opiniones para mostrar
        </div>
      </div>
    </section>

    <table v-else class="table table-light table-striped">
      <thead>
      <tr>
        <th>#</th>
        <th>Persona</th>
        <th>Juego</th>
        <th>Opinion</th>
        <th colspan="2"></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(comment, i) in comments" :key="i">
        <th scope="row">{{ i + 1 }}</th>
        <td>{{ comment.user }}</td>
        <td>{{ comment.game }}</td>
        <td>{{ comment.opinion }}</td>
        <td><button class="btn btn-danger btn-sm" @click="borrar(i)">Eliminar</button></td>
        <td><router-link :to="`/editcomment/${i}`"><button class="btn btn-info btn-sm text-white">editar</button></router-link></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>
<script>

import { mapState, mapActions} from 'vuex'

export default {
  computed: {
    ...mapState({
      comments: (state) => {
        return state.comments
      }
    })
  },
  methods: {
     ...mapActions(['borrarComentario']),
    borrar(i){
    this.$confirm("Estás seguro de borrar este comentario?").then(() => {
      this.borrarComentario(i)
    })
     }
  },
}
</script>
