<template>
  <div class="class">
    <div class="login">
      <form @submit.prevent action method>
        <h3>Sign Up</h3>

        <label for="firstName">First Name</label>
        <input
          type="text"
          v-model="registreForm.firstName"
          placeholder="First Name"
        />

        <label for="lastname">Last Name</label>
        <input
          type="text"
          v-model="registreForm.lastName"
          placeholder="Last Name"
        />

        <label for="Email">Email</label>
        <input type="Email" v-model="registreForm.email" placeholder="Email" />

        <label for="password">Password</label>
        <input
          type="password"
          v-model="registreForm.password"
          placeholder="Password"
        />

        <input
          type="submit"
          class="hover:bg-zinc-100"
          value="Sign Up"
          @click="register()"
        />
        <a class="cursor-pointer hover:text-zinc-300" @click="Login()"
          >already have an account <span class="text-blue-500">Login</span></a
        >
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "SignupComponent",
  data() {
    return {
      registreForm: {
        firstName: "",
        lastName: "",
        email: "",
        password: "",
      },
    };
  },
  methods: {
    Login() {
      this.$router.push("login");
    },
    register() {
      var myHeaders = new Headers();
      myHeaders.append("Accept", "application/json");
      myHeaders.append("Content-Type", "application/x-www-form-urlencoded");
      var urlencoded = new URLSearchParams();
      urlencoded.append("firstName", this.registreForm.firstName);
      urlencoded.append("lastName", this.registreForm.lastName);
      urlencoded.append("email", this.registreForm.email);
      urlencoded.append("password", this.registreForm.password);
      urlencoded.append("password_confirmation", this.registreForm.password);
      fetch("http://localhost:8000/api/register", {
        method: "POST",
        headers: myHeaders,
        body: urlencoded,
      })
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          if (result) {
            this.Login();
            // result["email"] = this.usedEmail;
          }
        });
    },
  },
};
</script>

<style scoped>
.login {
  display: flex;
  align-items: center;
}
.class {
  background-image: linear-gradient(
      rgba(60, 60, 68, 0.5),
      rgba(69, 69, 60, 0.5)
    ),
    url("../../assets/img/books.jpg");
  height: 87vh;
  overflow-y: hidden;
  display: flex;
  justify-content: center;
  text-align: start;
}
form {
  /* height: 90%; */
  /* width: 100%; */
  background-color: #2c3e50c2;
  backdrop-filter: blur(10px);
  box-shadow: 0 0 40px rgba(8, 7, 16, 0.6);
  padding: 40px 55px;
}
form * {
  font-family: "Poppins", sans-serif;
  color: #ffffff;
  letter-spacing: 0.5px;
  outline: none;
  border: none;
}
form h3 {
  font-size: 32px;
  font-weight: 500;
  line-height: 42px;
}

label {
  display: block;
  margin-top: 10px;
  font-size: 16px;
  font-weight: 500;
}
input {
  display: block;
  height: 50px;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.07);
  border-radius: 3px;
  padding: 0 10px;
  margin-top: 8px;
  font-size: 14px;
  font-weight: 300;
}
::placeholder {
  color: #e5e5e5;
}
button {
  margin-top: 18px;
  margin-bottom: 8px;
  width: 100%;
  background-color: #ffffff;
  color: #080710;
  padding: 15px 0;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
}
a {
  font-weight: 100;
}
</style>