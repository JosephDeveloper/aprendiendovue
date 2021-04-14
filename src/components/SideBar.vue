<template>
    <aside id="sidebar">
            <div id="nav-blog" class="sidebar-item">
            <h3>Puedes hacer esto</h3>
            <router-link to='crear-articulo' class="btn btn-success">Crear articulo</router-link>
            </div>
            <div id="search" class="sidebar-item">
            <h3>Buscador</h3>
            <p>Encuentra el articulo que buscas</p>
            <form @submit="goSearch">
                <input type="text" name="search" v-model="searchString">
                <input class="btn" type="submit" name="submit" value="Buscar">
            </form>
            </div>
    </aside>
</template>

<script>
export default {
    name: 'Sidebar',
    data() {
        return {
            searchString: null
        }
    },
    methods: {
        goSearch(){
            this.$router.push('/buscador/'+this.searchString)
        }
    }
}
</script>