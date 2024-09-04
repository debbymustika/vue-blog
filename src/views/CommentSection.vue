<template>
    <div class="container">
      <h1>Komentar</h1>
      <div v-if="userLoggedIn">
        <textarea v-model="newComment" placeholder="Add a comment"></textarea>
        <button @click="submitComment" class="btn btn-primary">Kirim Komentar</button>
      </div>
      <ul>
        <li v-for="comment in comments" :key="comment.id">{{ comment.body }}</li>
      </ul>
    </div>
  </template>
  
  <script>  
  export default {
    props:['articleId'],
    data(){
        return{
            comments:[
                {id:1,body:'ini adalah comment ke 1.'},
                {id:2,body:'ini adalah contoh comment ke 2.'}
            ],
            newComment:'',
            userLoggedIn:false
        };
    },
    created(){
        this.checkLoginStatus();
    },
    methods:{
        submitComment(){
            if(this.newComment.trim()==='')return;
            const newComment = {
                id:this.comments.length+1,
                body:this.newComment
            };
            this.comments.push(newComment);
            this.newComment='';
        },
        checkLoginStatus(){
            const user = JSON.parse(localStorage.getItem('user'));
            if(user &&user.token){
                this.userLoggedIn=true;
            }else{
                this.userLoggedIn=false;
            }
        },
    }
  }
  </script>
  