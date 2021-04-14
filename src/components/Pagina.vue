<template>
    <div class="general">
        <Slider texto='Pagina de Pruebas'/>
        <div class="center">
            <section id="content">  
                <h2 class="subheader">Pagina de Pruebas</h2>
                <h3>{{id_url}}</h3>
                <button @click="actualizarNombre">Actualizar nombre</button>
                <button @click="redirigirBlog">Redirigir</button>
                <h4>{{nombre}}</h4>
            </section>
            <Sidebar/>
        </div>
    </div>
</template>

<script>

import Slider from './Slider'
import Sidebar from './SideBar'

export default {
    name: 'Pagina',    
    components: {
        Slider,
        Sidebar
    },
    created(){
        console.log('Componente creado')
    },
    mounted(){
        this.id_url = this.$route.params.id
        console.log('Componente montado')
    },
    updated() {
        console.log('Componente actualizado')
    },
    destroyed() {
        console.log('Componente eliminado')        
    },
    data(){
        return {
            id_url: null,
            nombre: 'Joseph'
        }
    },
    methods: {
        actualizarNombre(){
            this.nombre = 'Joseph Lopez'
            console.log(this.nombre)
        },
        redirigirBlog(){
            this.$router.push('/blog')
        }
    }
}
</script>