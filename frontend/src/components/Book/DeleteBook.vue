<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col">
                <h3>
                    ¿Do you want to delete this book?
                </h3>
                <p>Title: {{ this.element.title }}</p>
                <p>Description: {{ this.element.description }}</p>

            </div>
        </div>
    <div class="row">
    <div class="col">
      <b-button v-on:click="deleteBook" variant="danger">Delete</b-button>
    </div>

    </div>
    </div>




</template>

<script>
import axios from 'axios'
import swal from 'sweetalert'
export default {
    data(){
        return {
          bookId: this.$route.params.bookId,
            element:
            {
                title: '',
                description: ''
            }
        }
    },
  methods:{
    getBook(){
        const path = `${process.env.BASE_URI}books/${this.bookId}/`
     axios.get(path)
          .then((response)=>{
            this.element.title = response.data.title
            this.element.description = response.data.description
          })
          .catch((error)=>{
            console.log(error);
          });
    },
    deleteBook(){
      const path = `${process.env.BASE_URI}books/${this.bookId}/`
      axios.delete(path)
           .then((response)=>{
             location.href='/books'
      })
      .catch((error)=>{
        swal("We can't delete the book","","error")
      })
    }
  },

  created(){
    this.getBook();
  }
}
</script>

<style lang="css" scoped>

</style>
