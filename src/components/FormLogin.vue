<template>
    <div class="wrapper-form">
      <form>
            <div class="mb-4">
                <label for="exampleInputEmail1" class="form-label">Форма входа</label>
                <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Введите Email" @blur="emailTouched = true" v-model="email" :class="{'br-warning': !email && emailTouched || incorrectDataEmail}">
                <div id="emailHelp" class="form-text" v-show="isLogin" :class="{'warning-text': isLogin}">{{messageEmail}}</div>
            </div>
            <div class="mb-4">
                <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Введите Пароль" autocomplete="on" @blur="passTouched = true" v-model="password" :class="{'br-warning': !password && passTouched || incorrectDataPass}">
                <div id="emailHelp" class="form-text" v-show="isLogin" :class="{'warning-text': isLogin}">{{messagePassword}}</div>
                <div id="emailHelp" class="form-text"></div>
            </div>
            <div class="wrap-button">
              <button type="submit" class="btn btn-primary" @click.prevent="isLogin">Войти</button>
              <div id="passwordHelpBlock" class="form-text form-text-login">
                <router-link to="/registration">Регистрация</router-link>
              </div>
            </div>
        </form>
    </div>
</template>

<script>
  const correctLogin = 'admin@admin.ru'
  const correctPass = '123'

  function getCookie(name) {
    let value = '; ' + document.cookie
    let parts = value.split('; ' + name + '=')

    if (parts.length == 2) return parts.pop().split(';').shift()
  }

  function isCookieExist() {
    document.cookie.indexOf('log_c') != '-1' ? true : false
  }

  function isValid(email) {
    const reg = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/

    return reg.test(email)
  }

  export default {
    name: 'FormLogin',
    data() {
      return {
          email: '',
          password: '',
          messageEmail: '',
          messagePassword: '',
          emailTouched: false,
          passTouched: false,
          incorrectDataEmail: false,
          incorrectDataPass: false
      }
    },
    methods: {
      isLogin() {
        if (this.email != '' && this.password != '') {
          if (!isValid(this.email)) {
            this.messageEmail = 'Некорректный Email'
            this.incorrectDataEmail = true

            this.messagePassword = ''
            this.incorrectDataPass = false
          } else {
            if (this.email === correctLogin && this.password === correctPass) {
              document.cookie = `log_c=${true}`

              this.$router.push('/')
            } else {
              this.messagePassword = 'Неправильный логин или пароль'
              this.messageEmail = ''
              this.incorrectDataEmail = true
              this.incorrectDataPass = true
            }
          }
        } else {
          if (this.email === '') {
            this.incorrectDataEmail = true
            this.messageEmail = 'Поле не должно быть пустым'
          } else {
            if (!isValid(this.email)) {
              this.messageEmail = 'Некорректный Email'
              this.incorrectDataEmail = true
            } else {
              this.incorrectDataEmail = false
              this.messageEmail = ''
            }
          }

          if (this.password === '') {
            this.messagePassword = 'Поле не должно быть пустым'
            this.incorrectDataPass = true
          } else {
            this.messagePassword = ''
            this.incorrectDataPass = false
          }
        }
      }
    }
  }
</script>

<style lang="scss">
  .wrapper-form {
    width: 100%;
    max-width: 300px;
  }

  .form-text-login {
    margin-left: 20px;
  }
</style>