<template>
    <div class="admin-post-page">
        <section class="update-form">
            <AdminPostForm
                :post="loadedPost"
                @submit="onSubmitted"
             />
        </section>
    </div>
</template>
<script>
import AdminPostForm from '@/components/admin/AdminPostForm'
import dbx from '~/modules/dbx.js'

export default {
    data(){
        return{
            id: '',
            loadedPost: []
        }
    },
    layout: 'admin',
    middleware: ['check-auth','auth'],    
    components: {
        AdminPostForm
    },
    asyncData(context){
       return context.app.$axios
            .$get(
                "/posts/" +
                context.params.postID +
                ".json"
            )
            .then(data => {

                return {
                    loadedPost: { ...data, id: context.params.postID }
                }
                 
            })
            .catch( e => context.error());

    },
    // created(){
    //     this.id = this.$store.getters.currentPost;
    //     console.log(this.id + ' id post')
    //     this.$axios.$get(
    //     '/posts/' +
    //     this.id +
    //     '.json')
    //     .then( data => {
        
        
    //         this.loadedPost = data;
    //         this.id = data.id;
        
    //     })
    //     .catch( e => console.log(e))
    // },
    methods: {
        onSubmitted(editedPost){
            this.$store.dispatch('editPost', editedPost)
            .then(() => {
                this.$router.push('/admin')
            });
        }
    }
};
</script>
