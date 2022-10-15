<template>

  <section class="src-components-http-client">
     <div class="jumbotron">
    <h1>Usuarios</h1>
    <button class="btn btn-warning my-3 mr-3" @click="getPostsXHRCb()">Pedir por http request</button>
    <button class="btn btn-secondary my-3 mr-3" @click="getPostsFetch()">Pedir por fetch</button>
    <button class="btn btn-success my-3 mr-3" @click="getPostsAxios()">Pedir por axios</button>
    <button class="btn btn-danger my-3 mr-3" @click="posts=[]">Clear</button>
    <br>
     <hr>
    <table v-if="posts.length" class="table table-dark">
      <tr>
        <th>Nombre</th>
        <th>Telefono</th>
        <th>Email</th>
      </tr>
      <tr v-for="(post,index) in posts" :key="index">
        <td>{{post.Nombre}}</td>
        <td>{{post.Telefono}}</td>
        <td>{{post.Email}}</td>
      </tr>
    </table>
    <h2 v-else class="alert alert-danger text-center">no se encuentran datos</h2>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-http-client',
    props: [],
    mounted () {

    },
    data () {
      return {
        url:"https://634271f73f83935a78433ad7.mockapi.io/Usuarios",
        posts:[ ],

      }
    },
    methods: {
      getPostsXHRCb(){
          const request =new XMLHttpRequest()
          request.open("get",this.url)

          request.addEventListener("load",()=>{
            if(request.status==200){
              let respuesta=JSON.parse(request.response)
              this.posts=respuesta

            }

          })

          request.send()
      },
      getPostsFetch(){
        fetch(this.url)//recibe una direccion
              .then(response => response.json())//devuelve una promesa
              .then(json =>{ this.posts = json})// no es necesario parsear
              .catch(error=>console.error(error))
      },
      getPostsAxios(){
        this.axios(this.url).then(respuesta=>{this.posts=respuesta.data}).catch(error=>console.error(error))
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
    .jumbotron{
    background-color: red;
    color: black;
  }
  hr{
    background-color: black;
  }
</style>
