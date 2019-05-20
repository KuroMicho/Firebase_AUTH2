<template>
  <div class="container-fluid">
    <div class="row">
      <div class="login-box">
        <img src="../img/logo2.png" class="avatar" alt="Avatar Image">
        <h1>Registrate Aqui</h1>
        <b-form @submit.prevent="registrarUsuario">
          <div class="col-sm-12">
            <b-form-group label="Email:" label-for="email">
              <b-input type="email" required placeholder="Ingrese su Email" v-model="form.email"/>
            </b-form-group>
          </div>

          <div class="col-sm-12">
            <!-- <label for="password">Password</label> -->
            <b-form-group label="Contraseña:" label-for="password">
              <b-input
                placeholder="Ingrese su contraseña"
                required
                type="password"
                v-model="form.password"
              />
            </b-form-group>
          </div>
          <input type="submit" value="Registrarse">
        </b-form>
      </div>
    </div>
  </div>
</template>  

<script>
import { auth } from "../services/firebase";

export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      }
    };
  },
  methods: {
    registrarUsuario() {
      if (this.form.password.length >= 6) {
        var user;
        user = auth
          .createUserWithEmailAndPassword(this.form.email, this.form.password)
          .catch(function(error) {
            // Handle Errors here.
            var errorCode = error.code;
            var errorMessage = error.message;
          });
        var email;
        user = auth.currentUser;
        if (this.form.email == user.email) {
          alert("El correo ya se ha registrado");
        } else {
          user
            .sendEmailVerification()
            .then(function() {
              alert("Email Enviado");
            })
            .catch(function(error) {
              // An error happened.
            });
        }
      } else {
        alert("Contreseña debil");
      }
    }
  }
};
</script>

<style>
.container-fluid {
  margin: 0;
  padding: 0;
  background: url(../img/bg.jpeg) no-repeat center top;
  background-size: cover;
  font-family: sans-serif;
  height: 100vh;
}

.login-box {
  width: 320px;
  height: 360px;
  background: #fff;
  color: #000;
  top: 60%;
  left: 50%;
  position: absolute;
  transform: translate(-50%, -50%);
  box-sizing: border-box;
  padding: 70px 30px;
}

.login-box .avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  position: absolute;
  top: -50px;
  left: calc(50% - 50px);
}

.login-box h1 {
  margin: 0;
  padding: 0 0 20px;
  text-align: center;
  font-size: 22px;
}

.login-box label {
  margin: 0;
  padding: 0;
  font-weight: bold;
  display: block;
}

.login-box input {
  width: 100%;
  margin-bottom: 20px;
}

.login-box input[type="email"],
.login-box input[type="password"] {
  border: none;
  border-bottom: 1px solid #000;
  background: transparent;
  outline: none;
  height: 40px;
  color: #000;
  font-size: 16px;
}

.login-box input[type="submit"] {
  border: none;
  outline: none;
  height: 40px;
  background: #b80f22;
  color: #fff;
  font-size: 18px;
  border-radius: 20px;
}

.login-box input[type="submit"]:hover {
  cursor: pointer;
  background: #ffc107;
  color: #000;
}

.login-box a {
  text-decoration: none;
  font-size: 12px;
  line-height: 20px;
  color: darkgrey;
}

.login-box a:hover {
  color: #fff;
}
</style>


