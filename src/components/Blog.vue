<template>
    <div class="general">
        <Slider texto='Blog'/>
        <div class="center">
            <section id="content">  
                <h1 class="subheader">Blog</h1>
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
    name: 'Blog',
    components: {
        Slider,
        Sidebar,
        Articles
    },
    mounted() {
        this.getArticles()
    },
    data() {
        return {
            articles: [],
            url: Global.url
        }
    },
    methods: {
        getArticles(){
            axios.get(this.url+'articles')
                .then(res => {
                    if(res.data.status == 'success') {
                        this.articles = res.data.articles                        
                    }
                })
        }
    },
}
</script>