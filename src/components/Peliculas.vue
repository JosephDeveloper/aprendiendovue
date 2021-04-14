<template>
    <div class="general">
        <Slider texto='Peliculas'/>
        <div class="center">
            <section id="content">
                <h1 class="subheader">Peliculas</h1>

                <div class="favorita" v-if="favorita">
                    <h2>{{favorita.title}}</h2>
                </div>

                <h3>{{ nombre | mayusculas }}</h3>

                <div id="articles">
                    <div v-for="pelicula in peliculasMayuscula" v-bind:key="pelicula.title">
                        <Pelicula
                            :pelicula="pelicula"
                            @favorita='haLlegadoLaPeliculaFavorita'
                        />
                    </div>
                </div>
            </section>
            <Sidebar/>
        </div>
    </div>
</template>

<script>

import Slider from './Slider'
import Sidebar from './SideBar'
import Pelicula from './Pelicula.vue'

export default {
    name: 'Peliculas',
    components: {
        Pelicula,
        Slider,
        Sidebar
    },
    methods: {
        haLlegadoLaPeliculaFavorita(favorita){
            this.favorita = favorita
        }
    },
    filters:{
        mayusculas(value){
            return value.toUpperCase()
        }
    },
    computed: {
        peliculasMayuscula(){
            var peliculasModificadas = this.peliculas
            for(var i = 0; i < this.peliculas.length; i++){
                peliculasModificadas[i].title = this.peliculas[i].title.toUpperCase()
            }
            return peliculasModificadas
        }
    },
    data() {
        return {
            nombre: 'Joseph Lopez',
            favorita: null,
            peliculas: [
                { title: 'Batman', year: 2017, image: 'https://image.api.playstation.com/vulcan/img/rnd/202010/2621/H9v5o8vP6RKkQtR77LIGrGDE.png?w=440'},
                { title: 'Teletubies', year: 1980, image: 'https://i2.wp.com/hipertextual.com/wp-content/uploads/2020/11/Teletubbies-Windows-XP-Wallpaper.jpg?fit=1500%2C1000&ssl=1'},
            ]
        }
    },
}
</script>