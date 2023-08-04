<template>
    <div>
      <Header />
        <div class="container">
            <form action="" class="form-horizontal">
                
                <div class="form-group left row" style="margin-top: 20px;">
                  <div class="col">
                        <label for="" class="control-label col-sm-3">Nombre</label>
                        <div class="col-sm-7">
                            <input type="text" class="form-control" name="nombre" id="nombre" v-model="form.nombre">
                        </div>
                    </div>
                    <div class="col">
                      <label for="" class="control-label col-sm-5">Cantidad</label>
                      <div class="col-sm-7">
                          <input type="text" class="form-control" name="cantidad" id="cantidad" v-model="form.cantidad">
                      </div>
                    </div> 
                </div>
                <div class="form-group left row">
                     <div class="col">
                        <label for="" class="control-label col-sm-2">Precio</label>
                        <div class="col-sm-7">
                            <input type="text" class="form-control" name="precio" id="precio" v-model="form.precio">
                        </div>
                      </div>
                     <div class="col">
                          <label for="" class="control-label col-sm-2">Categoria</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="categoria" id="categoria" v-model="form.categoria">
                          </div>
                    </div>
                </div>
                
                <div class="form-group" >
                  <button type="button" class="btn btn-primary" style="margin-top:15px" v-on:click="editar()" >Editar</button>                  
                </div> 
            </form>
        </div>
      <!-- <Footer />   -->
    </div>

</template>
<script>
    import Header from '@/components/Header.vue';
    import axios from 'axios';
    export default {
        name:"Editar",
        components:{
            Header
        },
        data:function(){
            return{
                id:null,
                form:{
                    "nombre" : "",
                    "cantidad" : "",
                    "precio" : "",
                    "categoria" : "" 
                }
            }
        },
        methods:{
            editar(){
                axios.put('http://127.0.0.1:8000/api/producto/update/'+this.id, this.form).then( data =>{
                    this.$router.push('home');
                });
            }
        },
        mounted:function(){
            this.id= this.$route.params.id;
            axios.get('http://127.0.0.1:8000/api/producto/'+this.id, this.form.id).then(
                datos => {
                    console.log(datos);
                    this.form.nombre = datos.data.nombre
                    this.form.cantidad = datos.data.cantidad
                    this.form.precio = datos.data.precio
                    this.form.categoria = datos.data    .categoria
                    
                }
            )
        }
    }
    
</script>

<style scoped>
 .left{
   text-align: left;
 };
 .margen{
   margin-left: 15px;
   margin-right: 15px;;
 }
</style>