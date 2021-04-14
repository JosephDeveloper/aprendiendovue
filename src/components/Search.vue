<template>
    <div class="general">
        <Slider :texto="'Busqueda: '+ searchId"/>
        <div class="center">
            <section id="content">  
                <h1 class="subheader" v-if="articles!=''">Articulos encontrados</h1>
                <h2 class="subheader" v-else>Sin resultados</h2>
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
    name: 'Search',
    components: {
        Slider,
        Sidebar,
        Articles
    },
    mounted() {
        this.searchId = this.$route.params.searchString
        this.getArticlesBySearch(this.searchId)
    },
    data() {
        return {
            articles: [],
            url: Global.url,
            searchId: null
        }
    },
    methods: {
        getArticlesBySearch(searchString){
            axios.get(this.url+'search/'+searchString)
                .then(res => {
                    if(res.data.status == 'success') {
                        this.articles = res.data.articles
                    }else{
                        this.articles = []
                    }
                })
        }
    },
}
</script>