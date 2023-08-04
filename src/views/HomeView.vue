<template>

  <nav class="navbar navbar-expand-lg navbar-dark bg-success">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Ecommerce</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link to="/" class="nav-link active" aria-current="page" href="#">Productos</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/create" class="nav-link" href="#">Crear</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/create" class="nav-link" href="#">Salir</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>


  
  <div class="row">
    <div class="col-lg-8 offset-lg-2">
      <div class="table-responsive">
        <table class="table table-light table-bordered table-hover">
          <thead>
            <tr>
              <th>#</th>
              <th>Nombre Producto</th>
              <th>Cantidad Disponible</th>
              <th>Precio</th>
              <th>Categoria</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody class="table-group-divider" id="contenido">
            <tr v-for="producto, i in products" :key="producto.id">
              <td>{{ (producto.id) }}</td>
              <td>{{ producto.nombre }}</td>
              <td>{{ producto.cantidad }}</td>
              <td>${{ new Intl.NumberFormat('es-mx').format(producto.precio) }}</td>
              <td>{{ producto.categoria }}</td>
              <td>
                <router-link :to="{path:'edit/'+producto.id}" class="btn btn-info">
                  <i class="fa-solid fa-edit"></i>
                </router-link>
                <button class="btn btn-danger" v-on:click="eliminar(producto.id)">
                  <i class="fa-solid fa-trash"></i>
                </button>
              </td>
            </tr> 
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <div class="container-fluid mt-3">
      <router-view/>
      
  </div>
</template>

<script>
  import Header from '@/components/Header.vue';
  //import la libreria para hacer la peticion
  import router from '@/router';
  import axios from 'axios';
  //crear funcion
  export default{    
    data() {
        return { products: null };
    },
    mounted() {
        this.getProductos();
    },
    methods: {
        getProductos() {
            //Hacemos el llamado al api usando el metodo get
            axios.get('http://127.0.0.1:8000/api/producto/').then(response => (this.products = response.data));
        },
        eliminar(id){
          
          axios.delete('http://127.0.0.1:8000/api/producto/delete/'+id).then(
              datos => {
                this.$router.go("/home");
              });
          

        }
    },
    components: { router }
}
</script>

