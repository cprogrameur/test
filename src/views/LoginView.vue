<template>
  <div class="flex flex-col h-screen justify-center items-center">
    <div class="max-w-sm mx-auto md:px-10 p-4 w-full">
      <div>
        <!-- logo -->
        <div
          class="flex justify-center mb-12"
          uk-scrollspy="target: > *; cls: uk-animation-scale-up; delay: 100 ;repeat: true"
        >
          <!-- <img
            src="assets/images/logo.png"
            alt=""
            class="w-auto h-16 shrink-0 bg-fuchsia-100 px-3 rounded-2xl p-2.5"
          /> -->
        </div>

        <form
          @submit.prevent="login"
          method="#"
          action="#"
          class="space-y-3"
          uk-scrollspy="target: > *; cls: uk-animation-scale-up; delay: 100 ;repeat: true"
        >
          <input
            class="!w-full h-10 border-gray-400 border-2 rounded-md p-1"
            v-model="email"
            type="email"
            placeholder="Email"
            autofocus=""
            required=""
          />
          <input
            class="!w-full h-10 border-gray-400 border-2 rounded-md p-1"
            v-model="password"
            type="password"
            placeholder="Password"
            autofocus=""
            required=""
          />

          <a href="#" class="hidden">
            <div class="text-sm text-right text-gray-400 py-4">Forget password</div>
          </a>

          <button
            type="submit"
            class="font-medium w-full hover:bg-white hover:border-slate-900 hover:border-2 hover:text-slate-900 rounded-lg bg-slate-900 py-1.5 px-4 text-white h-[38px] active:scale-[0.97] transition-all duration-150"
          >
            <span>Sign in</span>
          </button>
          <a type="button" :href="`https://orcid.org/oauth/authorize?client_id=APP-3UG1KEV436UMTXBJ&response_type=code&scope=/authenticate&redirect_uri=https://scinethub.netlify.app/oauth`"
            class="font-medium text-center hover:bg-white hover:border-blue-900 hover:border-2 hover:text-blue-900  w-full rounded-lg bg-blue-900 py-1.5 px-4 text-white h-[38px] active:scale-[0.97] transition-all duration-150">
            <span>Sign in with ORCID</span> </a>

          <div class="space-x-2 text-sm text-center text-slate-400 dark:text-white/70">
            <span> No account? </span>
            <span>—</span>
            <router-link to="/register" class="text-gray-600 hover:text-gray-500">Join now</router-link>
          </div>
          <p class="text-center">
            <a href="forget" class="text-gray-600 text-sm text-center hover:text-gray-500"
              >Forgot Password ?</a
            >
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    login() {
      const userData = {
        email: this.email,
        password: this.password,
      };


      axios.post('https://pydev-sac.yes.bj/api/login', userData)
        .then(response => {
          // Gérer la réponse du backend ici
          localStorage.setItem('token', response.data.data.token);
          console.log(response.data.data.token);
          this.$router.push('/profil');
          // Rediriger l'utilisateur ou effectuer d'autres actions en fonction de la réponse
        })
        .catch(error => {
          // Gérer les erreurs ici
          console.log(error);
        });
    },
  },
};
</script>