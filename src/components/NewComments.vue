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

    <section v-else>
      <div class="container">
        <div class="accordion accordion-flush" id="accordionFlushExample">
          <div class="accordion-item my-4" v-for="(comment, i) in comments" :key="i">
            <h2 class="accordion-header" :id="`heading${i}`">
              <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
                      :data-bs-target="`#collapse${i}`" aria-expanded="false" :aria-controls="`collapse${i}`">
                Opinión creada por "<span class="fw-bold">{{ comment.user }}</span>" para el juego "<span
                  class="fw-bold">{{ comment.game }}</span>"
              </button>
            </h2>
            <div :id="`collapse${i}`" class="accordion-collapse collapse border" :aria-labelledby="`heading${i}`"
                 data-bs-parent="#accordionFlushExample">
              <div class="accordion-body"><p><span class="fw-bold">Opinión: </span> {{ comment.opinion }}</p></div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>

import {mapState} from 'vuex'

export default {
  computed: {
    ...mapState({
      comments: (state) => {
        return state.comments
      }
    })
  }
}
</script>
