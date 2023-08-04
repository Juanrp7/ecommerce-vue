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
                  <button type="button" class="btn btn-primary"  v-on:click="guardar()">Guardar</button>
                  <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>                  
                </div> 
            </form>
        </div>

    </div>

</template>

<script>
    import Header from '@/components/Header.vue';
    import axios from 'axios';
    export default {
        name:"Nuevo",
        components:{
            Header
        },
        data:function(){
            return{                
                form:{
                    "nombre" : "",
                    "cantidad" : "",
                    "precio" : "",
                    "categoria" : "" 
                }
            }
        },
        methods:{
            guardar(){                
  
                axios.post("http://127.0.0.1:8000/api/producto/create",this.form)
                .then(data =>{
                    this.$router.push("/home");
                }).catch( e =>{
                    console.log(e);                  
                })  
            },
            salir(){
                this.$router.push("/home");
            },
          
        },
        
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