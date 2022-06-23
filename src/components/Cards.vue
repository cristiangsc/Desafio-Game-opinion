<template>
  <div class="row row-cols-1 row-cols-md-3 g-4 m-0">
    <div class="col" v-for="(game, i) in games" :key="i">
      <div class="card border-light h-100 m-2">
        <img :src="game.background_image" class="card-img-top" alt="...">
        <div class="card-body">
          <h3 class="card-title">{{ game.name }}</h3>
          <p class="card-text fw-bold">Rating: <span class="fw-lighter"> {{ game.rating }}</span></p>
          <p class="card-text fw-bold">Released<span class="fw-lighter">: {{ changeDate(game.released) }}</span></p>
          <p class="card-text fw-bold">Updated<span class="fw-lighter">:  {{ changeDate(game.updated) }}</span></p>
        </div>
        <div class="card-footer d-flex justify-content-center">
          <button type="button" class="btn btn-primary" data-bs-toggle="modal"
                  :data-bs-target="'#' + createIDs(game.name)">Opinar
          </button>

          <!-- Modal -->
          <div class="modal fade" :id="createIDs(game.name)" tabindex="-1" data-bs-backdrop="static"
               data-bs-keyboard="false" aria-hidden="true">
            <div class="modal-dialog modal-lg">
              <div class="modal-content">
                <div class="modal-header">
                  <h5 class="modal-title">Escribe tu opinión para el juego: <span class="fw-bold">{{ game.name }}</span>
                  </h5>
                  <button type="button" @click="cleanerOpinion" class="btn-close" data-bs-dismiss="modal"
                          aria-label="Close"></button>
                </div>
                <div class="modal-body">
                  <form>
                    <div class="mb-3">
                      <label class="col-form-label"><strong>Ingresa tu nombre:</strong></label>
                      <validation-provider rules="required" v-slot="v">
                        <input required type="text" v-model="gameOpinion.userName" class="form-control"
                               placeholder="Ingresa tu nombre">
                        <span>{{ v.errors[0] }}</span>
                      </validation-provider>
                    </div>
                    <div class="mb-3">
                      <label class="col-form-label"><strong>Ingresa tu opinión:</strong></label>
                      <validation-provider rules="required" v-slot="v">
                      <textarea required type="text" v-model="gameOpinion.userComment" class="form-control"
                                placeholder="Tu opinión debe ir aquí..."></textarea>
                        <span>{{ v.errors[0] }}</span>
                      </validation-provider>
                    </div>
                  </form>
                </div>
                <div class="modal-footer">
                  <button type="button" @click="addComment(game)" data-bs-dismiss="modal" class="btn btn-primary">
                    Guardar
                  </button>
                  <button type="button" @click="cleanerOpinion" class="btn btn-secondary"
                          data-bs-dismiss="modal">Cerrar
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState, mapActions} from 'vuex'
import {ValidationProvider, extend} from 'vee-validate';
import {required} from 'vee-validate/dist/rules';

extend('required', {
  ...required,
  message: 'El campo es requerido'
});

export default {
  components: {
    ValidationProvider
  },
  data() {
    return {
      gameOpinion: {
        userName: '',
        userComment: '',
        userGame: ''
      }
    }
  },
  computed: {
    ...mapState({
      games: (state) => {
        return state.games
      }
    }),
  },
  methods: {
    changeDate: (fecha) => {
      return (new Date(fecha).toLocaleDateString())
    },
    createIDs(gameName) {
      return `modal_${gameName.replace(/\s/g, '').replace(/:/g, '')}`
    },
    cleanerOpinion() {
      this.gameOpinion.userName = ''
      this.gameOpinion.userComment = ''
      this.gameOpinion.userGame = ''
    },

    ...mapActions(['agregarComentario']),
    addComment(game) {
      console.log(this.gameOpinion)
      if (this.gameOpinion.userComment !== '' || this.gameOpinion.userName!=='') {
        this.$alert("Su comentario ha sido registrado");
        this.gameOpinion.userGame = game.name
        this.agregarComentario(this.gameOpinion)
        this.cleanerOpinion()
      }
    }
  }
}
</script>
<style scoped>
img {
  object-fit: cover;
  height: 80%
}

textarea {
  height: 150px
}
</style>