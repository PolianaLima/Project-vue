<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <formToDo v-on:add-todo="addComment"></formToDo>      
    <div class="list-group">
      <p v-if="comments.length<=0">Sem Comentários</p>
      <div class="list-group-item" v-for="(comment, index) in allComments"  v-bind:key="index.comment">
        <span class="comment_author">Author: <strong>{{comment.name}}</strong> </span>
          <p>{{comment.message}}</p>
          <div>
            <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
          </div>
      </div>
    </div>
    <hr/>
    </div>
</template>

<script>
import formToDo from './formToDo';
export default{
  components:{
    formToDo
  },
  data(){
    return{
      comments:[]
    }
  },

  methods:{
    addComment(comment){
      this.comments.push(comment);
    },
      removeComment(index){
      this.comments.splice(index, 1);
    }
  },
  computed:{
    allComments (){
        return this.comments.map(Comment =>({
          ...Comment, 
          name: Comment.name.trim() === '' ? 'Anônimo' : Comment.name
        }))
      }
    },
    watch:{
      comments(val){
        console.log('val', val)
      }
    }
  }
</script>

