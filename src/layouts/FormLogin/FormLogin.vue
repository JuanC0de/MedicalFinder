<script>
  import { useField, useForm } from 'vee-validate'

  export default {
    data () {
      return {
        show2: false,
        password: 'Password',
        rules: {
          required: value => !!value || 'Requerido.',
          min: v => v.length >= 8 || 'Mínimo 8 caracteres',
          emailMatch: () => (`El correo electrónico y la contraseña introducidos no coinciden`),
        },
      }
    },
    setup () {
      const { handleSubmit } = useForm({
        validationSchema: {
          email (value) {
            if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true

            return 'Debe ser un correo electrónico válido.'
          },
        },
      })
      const email = useField('email')

      const submit = handleSubmit(values => {
        alert(JSON.stringify(values, null, 2))
      })

      return { email, submit }
    },
  }
</script>

<template>
  <v-card title="Iniciar Sesión" class="formContainer">
    <form @submit.prevent="submit">
      <v-text-field
        v-model="email.value.value"
        :error-messages="email.errorMessage.value"
        label="Correo electrónico"
      ></v-text-field>

      <v-text-field
              :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show2 ? 'text' : 'password'"
              name="input-10-2"
              label="Contraseña"
              hint="Al menos 8 caracteres"
              class="input-group--focused"
              @click:append="show2 = !show2"
            ></v-text-field>
      <v-container>
        <v-row justify="center">
          <v-col>
            <v-btn
              class="me-4"
              type="submit"
            >
              Enviar
            </v-btn>
          </v-col>
        </v-row>
        <v-row justify="center">
          <v-col>        
            <v-text>
              ¿Olvidaste tu contraseña?
            </v-text>
          </v-col>
        </v-row>
        <v-row justify="center">
          <v-col>
            <v-text>
              ¿No tiene una cuenta? Cree una.
            </v-text>
          </v-col>
        </v-row>
      </v-container>
    </form>
  </v-card>
</template>

<style>
    .formContainer{
        /* margin: 5cm 8cm 2cm 4cm; */
        position: absolute;
        left: 35%;
        transform: translate(-50%, 20%); 
        width: 80%; 
        max-width: 500px; 
    } 
</style>