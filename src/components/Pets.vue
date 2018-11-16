<template>
  <div class="content">
    <h1>Mascotas</h1>
    <hr>
    <table>
      <thead>
        <tr>
          <th>Nombres</th>
          <th>Tipos</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pet in pets">
          <td>
            <div v-if="!pet.editing" @dblclick="editpet(pet)">{{ pet.name }}</div>
            <input v-else class="pet-item-edit" type="text" v-model="pet.name" @keyup.enter="doneEdit(pet)">
          </td>
          <td>
            <div v-if="!pet.editing" @dblclick="editpet(pet)">{{ pet.type }}</div>
            <input v-else class="pet-item-edit" type="text" v-model="pet.type" @keyup.enter="doneEdit(pet)">
          </td><button class="btn btn-danger btn-sm" @click="deletePet(pet)">X</button>
        </tr>
      </tbody>
    </table>
    <div>
  	   <form class="form-inline mt-5">
  		     <div class="form-group mx-sm-3">
  		    		<input type="text" class="form-control mr-2" v-model="petnew.name" placeholder="nombre de mascota">
  				    <input type="text" class="form-control" v-model="petnew.type" placeholder="tipo de la mascota" @keydown.enter="savepet">
  		    </div>
  		    <button type="button" class="btn btn-success" @click.prevent="savepet">Agregar</button>
  		</form>
  	</div>
    <div class="alert alert-warning" id="helptext">
      <h2></h2>
      <p>Para editar por favor dar doble click sobre la mascota y guarda con la tecla Enter</p>
    </div>
  </div>
</template>
<script>
const STORAGE_KEY = 'pet-storage';
export default {
  name: 'Pets',
  data () {
    return {
      petnew: {editing:false},
      pets: [{}],
    }
  },
  methods: {
		savepet(){
			this.pets.push(this.petnew);
      this.petnew = {editing:false};
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.pets));
		},
    deletePet(pet){
      this.pets.splice(this.pets.indexOf(pet), 1);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.pets));
    },
    editpet(pet){
      pet.editing = true
    },
    doneEdit(pet){
      pet.editing = false
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.pets));
    }
	},
  created() {
    this.pets = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  table {
    width: 90%;
    margin: 0 auto;
  }
  th, td {
    text-align: center;
    width: 30%;
  }
  .content{
    max-width: 50%;
    margin: 0 auto;
  }
  h1{
    text-align: center;
    color: red;
  }
  ul
  {
    list-style-type: none;
  }

  .pet-item-edit{
    font-size: 15px;
    color: #2c3e50;
    width: 100%;
    border: 1px solid #ccc;
  }

  #helptext{
    margin-top: 20px;
    font-style: italic;
    text-align: center;
  }

</style>
