<template>
    <section id="content">  
        <h2 class="subheader">{{titulo}}</h2>
        <h1>Este es mi componente</h1>
        <h2>{{ subtitulo }}</h2>

        <h2>Reactividad</h2>
        <input type="text" v-model="nombre">
        Mi nombre es: <strong>{{nombre}}</strong>
        <pre>
            {{$data}}
        </pre>

        <h2>Condicionales</h2>
        <input type="number" v-model="edad">
        Mi edad es: <strong>{{edad}}</strong>

        <p style="color: green; font-weight: bold;" v-if="edad && edad>=18 && edad<65">Eres mayor de edad</p>
        <p style="color: red; font-weight: bold;" v-else-if="edad && edad>=65">Eres de tercera edad</p>
        <p style="color: red; font-weight: bold;" v-else>Eres menor de edad</p>

        <h2>Iteraciones</h2>
        <ol>
            <li v-for="pelicula in peliculas" :key="pelicula">
                {{pelicula}}
            </li>
        </ol>
    </section>
</template>

<script>
export default {
    name: 'MiComponente',
    data(){
        return {
            titulo: 'Mi Componente',
            subtitulo: 'Soy yo',
            nombre: '',
            edad: 18,
            peliculas: ['Batman', 'Señor de los anillos', 'Spiderman']
        }
    }
}
</script>