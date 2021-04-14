<template src="./CreateArticle.html"></template>

<script>

import axios from 'axios'
import { required } from 'vuelidate/lib/validators'
import Sidebar from './SideBar'
import Global from '../Global.js' //llaves cuando se exporta un modulo
import Article from '../models/Article'
import Swal from 'sweetalert2'

export default {
    name: 'EditArticle',
    components: {
        Sidebar
    },
    data() {
        return {
            url: Global.url,
            article: new Article('','',null,''),
            file: '',
            submitted: false,
            isEdit: true
        }
    },
    validations: {
        article: {
            title: {
                required
            },
            content: {
                required
            }            
        }
    },
    mounted() {
        var id = this.$route.params.id
        this.getArticle(id)
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
        save(){
            //console.log(this.article)
            this.submitted = true
            var id = this.$route.params.id

            if(this.$v.$invalid){
                return false
            }else{                
                axios.put(this.url+'article/'+id, this.article)
                    .then(res => {
                        if(res.data.status == 'success'){
                            //subida de archivo
                            if(this.file != null && this.file != undefined && this.file !=''){
                                const formData = new FormData()
    
                                formData.append(
                                    'file0',
                                    this.file,
                                    this.file.name
                                )
                                var id = res.data.article._id
                                axios.post(this.url+'upload-image/'+id, formData)
                                    .then(res => {
                                        if(res.data.article){
                                            Swal.fire({
                                                position: 'top-end',
                                                icon: 'success',
                                                title: 'Se ha editado correctamente',
                                                showConfirmButton: false,
                                                timer: 1500
                                            })
                                            this.article = res.data.article
                                            this.$router.push('/articulo/'+this.article._id)
                                        }else{
                                            //mostrar alerta de error
                                            Swal.fire({
                                                position: 'top-end',
                                                icon: 'error',
                                                title: 'Hubo un error al editar el articulo',
                                                showConfirmButton: false,
                                                timer: 1500
                                            })
                                        }
                                    })
                                    .catch(err =>{
                                        console.log(err)
                                    })
                            }else{
                                Swal.fire({
                                    position: 'top-end',
                                    icon: 'success',
                                    title: 'Se ha editado correctamente',
                                    showConfirmButton: false,
                                    timer: 1500
                                })
                                this.article = res.data.article
                                this.$router.push('/articulo/'+this.article._id)
                            }
                        }
                    })
                    .catch(err => {
                        console.log(err)
                    })             
            }

        },
        fileChange(){
            this.file = this.$refs.file.files[0]
        }
    },
}

</script>