<template>
  <div>
    <img src="@/assets/Frame.png" alt="" style="position: fixed; z-index: -1"/>
    <v-container>
      <v-row justify="center">
        <v-col
          class="rounded-container"
          sm="4"
          md="4"
          lg="4"
          style="background: rgba(255,255,255,0.1); position: absolute; top: 45%; left: 50%;
        transform: translate(-50%, -50%);box-shadow: 0 0 2px rgba(0, 0, 0, 0);"
        >
          <img src="@/assets/AFR_рус.png" alt="" style="width: 300px">
          <v-form
            ref="form"
            v-model="valid"
            @keyup.enter.native="submit">
            <v-text-field
              v-model="login"
              :rules="loginRules"
              label="Имя пользователя"
              prepend-icon="mdi-account"
              counter
              required>
            </v-text-field>
            <v-text-field
              v-model="password"
              :rules="passwordRules"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              :type="show ? 'text' : 'password'"
              prepend-icon="mdi-lock"
              counter
              label="Пароль"
              required
              @click:append="show = !show"
            ></v-text-field>
            <v-row style="justify-content: center; margin: 10px">
              <v-btn
                @click="submit"
                style="margin-top: 20px; color: white"
                color="rgb(41, 83, 122)"
              >
                Войти
              </v-btn>
            </v-row>
          </v-form>
        </v-col>
      </v-row>
      <v-snackbar
        v-model='snack'
        :timeout='3000'
        :color='snackColor'
      >
        {{ snackText }}
        <template #action='{ attrs }'>
          <v-btn
            v-bind='attrs'
            text
            @click='snack = false'
          >
            Закрыть
          </v-btn>
        </template>
      </v-snackbar>
    </v-container>
  </div>
</template>

<script>

export default {
  name: 'LoginPage',
  components: {
  },
  data: () => ({
    valid: false,
    query: [],
    login: '',
    password: '',
    checklogin: false,
    show: false,
    loginRules: [
      v => !!v || 'Обязательное поле'
    ],
    passwordRules: [
      v => !!v || 'Обязательное поле'
    ],
    snack: false,
    snackColor: '',
    snackText: '',
  }),
  created(){
  },
  methods: {
    async submit(){

      try {
        const login = {
          'username': this.login,
          'password': this.password
        }
        const response = await this.$auth.loginWith('local', {data: login})
        this.$router.push('/')
      } catch (error) {
        this.snack = true
        this.snackColor = '#942738'
        this.snackText = 'Неверные имя пользователя или пароль!'
        console.error(error); // Обработка ошибок аутентификации
      }
    }
  },
}
</script>
<style scoped>
.rounded-container {
  border-radius: 10px; /* Задайте радиус закругления в пикселях, как вам нужно */
  overflow: hidden; /* Убедитесь, что контент не выходит за пределы закругленных углов */
}
</style>
