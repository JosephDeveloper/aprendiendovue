<template>
    <div class="general">
        <Slider texto='Formulario'/>
        <div class="center">
            <section id="content">  
                <h2 class="subheader">Formulario</h2>
                <form action="" class="mid-form" @submit.prevent="mostrarUsuario">
                    <div class="form-group">
                        <label for="nombre">Nombre</label>
                        <input type="text" name="nombre" v-model="user.nombre">
                        <div v-if="submited && !$v.user.nombre.required">El campo es requerido</div>
                        <div v-if="submited && !$v.user.nombre.minLength">El campo debe tener más de 2 carácteres</div>
                    </div>
                    <div class="form-group">
                        <label for="apellido">Apellido</label>
                        <input type="text" name="apellido" v-model="user.apellidos">
                        <div v-if="submited && !$v.user.apellidos.required">El campo es requerido</div>
                        <div v-if="submited && !$v.user.apellidos.minLength">El campo debe tener más de 2 carácteres</div>
                    </div>
                    <div class="form-group">
                        <label for="bio">Biografia</label>
                        <textarea name="bio" v-model="user.bio"></textarea>
                        <div v-if="submited && !$v.user.bio.required">El campo es requerido</div>
                        <div v-if="submited && !$v.user.bio.minLength">El campo debe tener más de 10 carácteres</div>
                    </div>
                    <div class="form-group radiobuttons">
                        <input type="radio" name="genero" value="hombre" v-model="user.genero" checked>Hombre
                        <input type="radio" name="genero" value="mujer" v-model="user.genero">Mujer
                        <input type="radio" name="genero" value="otro" v-model="user.genero">Otro
                    </div>

                    <div class="clearfix"></div>

                    <input type="submit" value="Enviar" class="btn btn-success">
                </form>

                <div class="datos" v-if="user.nombre && user.apellidos">
                    <h3>{{user.nombre + user.apellidos}}</h3>
                </div>
            </section>
            <Sidebar/>
        </div>
    </div>
</template>

<script>

import { required, minLength } from 'vuelidate/lib/validators'
import Slider from './Slider'
import Sidebar from './SideBar'

export default {
    name: 'Formulario',
    components: {
        Slider,
        Sidebar
    },
    validations: {
        user: {
            nombre: {
                required,
                minLength: minLength(2)
            },
            apellidos: {
                required,
                minLength: minLength(2)
            },
            bio: {
                required,
                minLength: minLength(10)
            }
        }
    },
    methods: {
        mostrarUsuario(){
            console.log(this.user)
            this.submited = true
            /* this.$v.$touched() */
            if(this.$v.$isInvalid){
                return true
            }
        }
    },
    data() {
        return {
            submited: false,
            user: {
                nombre: '',
                apellidos: '',
                bio: '',
                genero: ''
            }
        }
    }
}
</script>