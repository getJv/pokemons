<template>
  <div class="modal fade" id="addPokemon" role="dialog" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Agregar Pokemon</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="savePokemon">
            <div class="form-group">
              <label>Pokemon</label>
              <input
                type="text"
                class="form-control"
                v-model="name"
                placeholder="Ingresa el nombre del pokemon"
              />
            </div>
            <div class="form-group">
              <label>Picture</label>
              <input
                type="text"
                class="form-control"
                v-model="picture"
                placeholder="Ingresa la url de una imagen"
              />
            </div>
            <button type="submit" class="btn btn-primary">Save</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script> 
import EventBus from './EventBusComponent';

export default {
  data() {
    return {
      name: null,
      picture: null
    }
  },
  methods: {
    savePokemon: function() {
      axios.post('http://localhost/pokemons',{
        name: this.name,
        picture:this.picture
      })
      .then(res => {
        EventBus.$emit('pokemon-added', res.data.pokemon)
        $('#addPokemon').modal('hide')
      })
      .catch(err => console.log(err));
      
    }
  }
};
</script>

