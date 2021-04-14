<template>
    <div class="general">
        <Slider texto='Bienvenido' home='true'/>
        <div class="center">
            <section id="content">
                <h2 class="subheader">Últimos articulos</h2>
                <div id="articles" v-if="articles">
                    <Articles :articles="articles"/>
                </div>
            </section>
            <Sidebar/>
        </div>
    </div>
</template>

<script>

import axios from 'axios'
import Slider from './Slider'
import Sidebar from './SideBar'
import Articles from './Articles'
import Global from '../Global.js' //llaves cuando se exporta un modulo

export default {
    name: 'LastArticle',
    components: {
        Slider,
        Sidebar,
        Articles
    },
    mounted() {
        this.getLastArticles()
    },
    data() {
        return {
            articles: [],
            url: Global.url
        }
    },
    methods: {
        getLastArticles(){
            axios.get(this.url+'articles/true')
                .then(res => {
                    if(res.data.status == 'success') {
                        this.articles = res.data.articles
                    }
                })
        }
    },
}
</script>