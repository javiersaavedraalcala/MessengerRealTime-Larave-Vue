<template>
  <div>
    <b-container >
        <b-form class="m-3" v-if="show" action="" method="post" enctype="multipart/form-data">
            <input type="hidden" name="_token" v-model="csrfToken">
             
            <b-form-group label="Correo electrónico" >
                <b-form-input
                    name="email"
                    v-model="user.email"
                    type="email"
                    readonly
                ></b-form-input>
            </b-form-group>

            <b-form-group  label="Nombre:" >
                <b-form-input
                    name="name"
                    v-model="user.name"
                    required
                ></b-form-input>
            </b-form-group> 

            <b-form-group  label="Nueva contraseña: (Opcional)" >
                <b-form-input
                    name="password"
                    type="password"
                ></b-form-input>
            </b-form-group> 

            <b-form-group  label="Imagen de perfil: (Opcional)" >
                <b-img class="m-1" :src="image" rounded="circle" width="60" heigth="60"></b-img>
                <b-form-file 
                    name="image"
                    placeholder="Sube nueva image" 
                ></b-form-file>
            </b-form-group> 

            <b-button type="submit" variant="primary">Guardar cambios</b-button>
        </b-form> 
    </b-container>
    
  </div>
</template>

<script>
  export default {
    props: {
        user: Object,
        csrfToken: String
    },
    data() {
      return { 
        show: true
      }
    },
    methods: {
      
    },
    computed: {
        image() {
            return `/users/${this.user.image}`;
        }
    }
  }
</script>