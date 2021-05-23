<template>
  <section class="src-components-http">
  
   <div class="container">
    <button class="btn btn-danger " @click="getPostsCb()">
      Pedir XMLHttpRequest
    </button>
    <button class="btn btn-warning " @click="getPostsFech()">
      Pedir Fetch
    </button>
    <button class="btn btn-success " @click="getPostAxios()">
      Pedir Axios
    </button>
 </div>

<hr>
    <tabla :posts="post" />
  
  </section>
</template>

<script lang="js">
import tabla from './tabla.vue'
  export default  {

  components: {
      tabla
   },
   name: 'src-components-http',
    props: [],

    mounted () {

    },
    data () {
      return {
        post:[],
        url:"https://60a9668c20a64100173071ea.mockapi.io/personas"

      }
    },
    methods: {
    getPostsCb(){
      const xhr = new XMLHttpRequest
      xhr.open('get',this.url)
      xhr.addEventListener('load',() => {
          if(xhr.status == 200){
            let respuesta = JSON.parse(xhr.response)
            this.post = respuesta
          }
        else{
        console.error(`Error GET : Status : ${xhr.status}`)
        }
      })
        xhr.addEventListener('error', e => {
          console.error('Error XMLHttpRequest ->',e)
        })
      
        xhr.send()
  
  },
  async getPostsFech(){
    try {
     const response =  await fetch(this.url)
      console.log(response)
      const datos = await response.json()
      this.post = datos
    } catch (error) {
      console.error(error)
    }
  },

   async getPostAxios(){
     try{
     const response = await this.axios(this.url)
    
        this.post = response.data
     }catch(error)
        {console.log(error)
   }
  }

      },
    computed: {

    }
}
</script>

<style scoped lang="css">
.src-components-http {

height: 93vh;
}
.container{
  display: flex;
  justify-content: space-around;
  padding-top: 20px;

  
}
hr{
  color: rgb(255, 0, 0);
}
</style>
