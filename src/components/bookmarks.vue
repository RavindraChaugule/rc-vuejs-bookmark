<template>
    <div>
        <div class="form-head">
            <div class="columns">
                <div class="column">
                    <input v-on:keyup.enter="addBookmark" v-model="newTitle" class="input" type="text" placeholder="Title">
                </div>
                <div class="column">
                    <input v-on:keyup.enter="addBookmark" v-model="newLink" class="input" type="text" placeholder="URL">
                </div>
                <div class="column is-one-fifth">
                    <button v-on:click="addBookmark" class="button is-primary bm-add">Add</button>
                </div>
            </div>
        </div>
        <div v-for="(bookmark, index) in bookmarks">
            <div v-show="bookmark.isEdit = !bookmark.isEdit" class="panel-block">
                <span class="icon is-small is-left">
                <i class="far fa-bookmark"></i>
                </span>

                <a class="bm-link" v-bind:href="bookmark.link">{{ bookmark.title }}</a>

                <span v-on:click="editBookmark(bookmark)" class="button is-info bm-delete is-small bm-edit">
                    <i class="fas fa-pencil-alt"></i> Edit
                </span>

                <span v-on:click="deleteBookmark(index)" class="button is-danger bm-delete is-small">
                    <i class="fas fa-times-circle"></i> Delete
                </span>
            </div>


            <div v-show="bookmark.isEdit = !bookmark.isEdit" class="edit-field">
                <input v-model="bookmark.title" class="input" type="text" placeholder="Title">
                <input v-model="bookmark.link" class="input" type="text" placeholder="URL">
                <button v-on:click="doneEdit(bookmark)" class="button is-primary bm-add">Done</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                newTitle: '',
                newLink: '',
                cachedTitle: '',
                cachedLink: '',
                bookmarks: [
                    {
                        title: 'Google',
                        link: 'http://google.com',
                        isEdit: false
                    },
                    {
                        title: 'Yahoo',
                        link: 'http://yahoo.com',
                        isEdit: false
                    },
                    {
                        title: 'Facebook',
                        link: 'http://facebook.com',
                        isEdit: false
                    }
                ]
            }
        },
        methods: {
            addBookmark: function(){
               if(this.newTitle.trim().length == 0 || this.newLink.trim().length == 0){
                   alert('!! Something is missing');
               }else{
                   this.bookmarks.push({
                       title: this.newTitle,
                       link: this.newLink,
                       isEdit:false
                   });                   
               }
               this.newTitle =  '';
               this.newLink =  '';
            },
            editBookmark: function(bookmark){
                //this.cachedTitle = bookmark.title;
                //this.cachedLink = bookmark.link;
                bookmark.isEdit = true
            },
            doneEdit: function(bookmark){
                if(bookmark.title.trim().length == 0 || bookmark.link.trim().length == 0){
                   alert('!! Something is missing');
                   //bookmark.title = this.cachedTitle
                   //bookmark.link = this.cachedLink
               }else{
                   bookmark.isEdit = false;
               }
            },
            deleteBookmark: function(index){
                this.bookmarks.splice(index, 1);
            }
        }
    }
</script>

<style>
.panel-block{
    border-bottom:1px solid #ddd;
}
.bm-link{
width: 100%;
color:#555;
text-transform: capitalize;
}
.bm-link:hover{
    color:#000;
}
.bm-edit{
margin-right:5px;
}
.button svg{
margin-right:4px;
}
.icon{
margin-right:5px;
}
.panel-block:first-child{
    border-top:0;
}
.form-head{
padding-bottom:20px;
border-bottom:1px solid #ddd;
  } 
  .bm-add{
      width: 100%;
  }
  .edit-field{
      padding:20px 15px;
      display: flex;
      border:1px solid #ddd;
      
      border-top:0;
  }
  .edit-field input{
      margin-right: 5px;
  }
</style>