<template>
    <div class="general">
        <Slider texto='Blog'/>
        <div class="center">
            <section id="content" v-if="article">  
                <article class="article-item article-detail">
                    <div class="image-wrap">
                        <img :src="url+'get-image/'+article.image"
                            :alt="article.title" v-if="article.image"/>
                        <img v-else src="../assets/images/image-not-found.png" :alt="article.title"/>
                    </div>
                    <h1 class="subheader">{{article.title}}</h1>
                    <span class="date">{{article.date | moment('from', 'now')}}</span>
                    <p>
                        {{article.content}}
                    </p>
                    <div class="clearfix"></div>
                    <router-link :to="'/editar/'+article._id" class="btn btn-warning">Editar</router-link>
                    <a @click="deleteArticle(article._id)" class="btn btn-danger">Eliminar</a>
                </article>
            </section>
            <SideBar/>
        </div>
    </div>
</template>

<script>

import axios from 'axios'
import Swal from 'sweetalert2'
import Slider from './Slider'
import SideBar from './SideBar'
import Global from '../Global'

export default {
    name: 'Article',
    components: {
        Slider,
        SideBar
    },
    data() {
        return {
            url: Global.url,
            article: null
        }
    },
    mounted() {
        var articleId = this.$route.params.id
        this.getArticle(articleId)
    },
    methods: {
        getArticle(articleId){
            axios.get(this.url+'article/'+articleId)
                .then(res => {
                    if(res.data.status == 'success'){
                        this.article = res.data.article
                    }
                })
        },
        deleteArticle(id){
            Swal.fire({
                title: 'Estas seguro?',
                text: "Deseas eliminar el articulo?",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#3085d6',
                cancelButtonColor: '#d33',
                confirmButtonText: 'Si'
            }).then((result) => {
                if (result.isConfirmed) {
                    axios.delete(this.url+'article/'+id)
                        .then(res => {
                            if(res.data.status == 'success'){
                                Swal.fire(
                                    'Eliminado!',
                                    'El articulo fue eliminado.',
                                    'success'
                                )
                                this.$router.push('/blog')
                            }else{
                                Swal.fire(
                                    'Error!',
                                    'Hubo un error al eliminar el articulo.',
                                    'error'
                                )
                                this.$router.push('/articulo/'+this.article._id)
                            }
                        })
                }
            })            
        }
    }
}
</script>