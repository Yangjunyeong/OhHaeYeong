<template>
  <div id="app">
    <nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top">
      <div class="container-fluid">
        <router-link :to="{name: 'home'}" class="navbar-brand"><img src="@/assets/byeongjin.jpg" alt="병진이" class="rounded" ></router-link>
        <router-link :to="{name: 'home'}" class="navbar-brand">오태식의 해바라기 영화</router-link>
  
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <router-link v-if="!isLogin" class="nav-link" :to="{ name: 'SignUpView' }"  >SignUp</router-link>
            </li>
            <li class="nav-item">
              <router-link v-if="!isLogin" class="nav-link" :to="{ name: 'LogInView' }" >LogIn</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" :to="{ name: 'MoviesView' }"  >Movies</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" :to="{ name: 'RandomView' }"  >Random</router-link>
            </li>
            <li class="nav-item">
              <a class="nav-link" v-if="isLogin" @click="logout">Logout</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    
    
    <router-view class="p-0"/>

    <footer>
      <br>

      <ul class="nav justify-content-center border-bottom pb-3 mb-3">
        <li class="nav-item"><router-link :to="{name: 'home'}" class="nav-link px-2 text-muted">Home</router-link></li>
        <li class="nav-item"><router-link :to="{name: 'MoviesView'}" class="nav-link px-2 text-muted">Movies</router-link></li>
        <li class="nav-item"><router-link :to="{name: 'RandomView'}" class="nav-link px-2 text-muted">RandomPick</router-link></li>       
      </ul>
      <p class="text-center text-muted">© 2023 Company, OhHaeYeong</p>
      <audio ref="audioPlayer" src="@/assets/sunflowersong.mp3" loop autoplay controls ></audio>
    </footer>
  
</div>


</template>

<script>
export default {
  name: 'App',
  computed: {
    isLogin() {
      return this.$store.getters.isLogin // 로그인 여부
    }, 
  },
  created() {

  },
  mounted() {
    const audio = this.$refs.audioPlayer;
    audio.volume = 0.4; // 초기 볼륨 설정 (0.5는 절반 크기)
  },
  methods: {
    logout() {
      this.$store.dispatch('logout');
    },
    openModal(movie) {
      this.selectedMovie = movie;
      this.isModalOpen = true;
    },
    playAudio() {
      const audio = this.$refs.audioPlayer;
      audio.play(); // 오디오 재생
    },
    closeModal() {
      this.isModalOpen = false;
    }, 
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
  
  ;
}

nav {
  padding: 30px;
  background-color: #2c3e50;
  
}

nav a {
  font-weight: bold;
  color: whitesmoke;
}

nav a.active {
  color: #42b983;
}

nav img {
  width: 40px;
  height: 40px;
  border-radius: 70%;
  margin-right: 10px;
}
.bd-placeholder-img {
  font-size: 1.125rem;
  text-anchor: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}

@media (min-width: 768px) {
  .bd-placeholder-img-lg {
    font-size: 3.5rem;
  }
}

.b-example-divider {
  height: 3rem;
  background-color: rgba(0, 0, 0, .1);
  border: solid rgba(0, 0, 0, .15);
  border-width: 1px 0;
  box-shadow: inset 0 .5em 1.5em rgba(0, 0, 0, .1), inset 0 .125em .5em rgba(0, 0, 0, .15);
}

.b-example-vr {
  flex-shrink: 0;
  width: 1.5rem;
  height: 100vh;
}

.bi {
  vertical-align: -.125em;
  fill: currentColor;
}

.nav-scroller {
  position: relative;
  z-index: 2;
  height: 2.75rem;
  overflow-y: hidden;
}

.nav-scroller .nav {
  display: flex;
  flex-wrap: nowrap;
  padding-bottom: 1rem;
  margin-top: -1px;
  overflow-x: auto;
  text-align: center;
  white-space: nowrap;
  -webkit-overflow-scrolling: touch;
}
.button {
  display: inline-block;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.button:hover {
  background-color: #0056b3;
}

</style>