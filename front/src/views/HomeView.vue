<template>
    <div class="home">
    <section class="d-flex justify-content-center">
    <h1 class="text-start main"> 나를 웃게 하는건 <br> "영화" 입니다</h1>
    
    <header class="masthead">
        <div class="container-fluid px-0">
            <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                <div class="col-lg-8 align-self-end">
                    <h1 class="text-white font-weight-bold">오태식의 해바라기 영화에 오신걸 환영합니다!!</h1>
                    <hr class="divider" />
                </div>
            
            <div class="container">
                <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                <div class="col-md-6 cardImg">
                    <img src="@/assets/comeback.png" alt="오태식이 돌아왔구나" class="img-fluid">
                </div>
                <div class="col-md-6">
                    <h2 class="mb-5 fw-bold">오태식이 돌아왔구나...</h2>
                    <h6>저희의 사이트에 돌아와줘서 감사합니다.</h6>
                    <h6>오.해.영에서 최신영화와 추천영화의 정보를 확인하십시오.</h6>
                </div>
                </div>
            </div>
            </div>
    </div>
                
    <br>
        
            <div class="container-fluid px-0 mb-5">
                <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                    <div class="col-lg-8 align-self-end">
                        <h1 class="text-white font-weight-bold">최신영화</h1>
                        <hr class="divider" />
                    </div>
                
                    <div class="container">
                    <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                        <div class="col-md-6">
                        <h2 class="mb-5 fw-bold">오... 오태식이</h2>
                            <h6>10년 동안 울면서 후회하고 다짐하느라</h6>
                            <h6>최신영화를 몰랐을 오태식을 위해 준비했습니다</h6>
                            <h6>최신영화 목록을 확인 하십시오.</h6>
                        </div>
                        <div class="col-md-6 cardImg">
                        <img src="@/assets/ohtaesik2.png" alt="오태식이 돌아왔구나" class="img-fluid">
                        </div>
                    </div>
                    </div>
                </div>
            </div>
    <div class="swiper-container">
    <swiper :options="swiperOptions" ref="swiper">
        
        <swiper-slide  v-for="(movie, idx) in recentMovies" :key="idx">
            <RecentMovie :movie="movie" @openModal="openModal(movie)"/>
        </swiper-slide>
        
        <div class="swiper-button-next" slot="button-next"></div>
        <div class="swiper-button-prev" slot="button-prev"></div>
    </swiper>
    </div> 
    <!-- 모달 창 -->
    <div v-if="isModalOpen" class="modal" @click="closeModal">
        <div class="modal-content" @click.stop>
            <img
            v-bind:src="`https://image.tmdb.org/t/p/original${selectedMovie.poster_path}`"
            class="modal-poster"
            alt="image"
            style="border-radius: 10px"
            />
            <p class="modal-title text-black"><strong>{{  selectedMovie.title }}</strong> <br>
                <span class="overview-text">{{ selectedMovie.overview }}</span>
            </p>
        </div>
    </div>
        


    <br>
        <div class="container-fluid px-0">
            <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                <div class="col-lg-8 align-self-end">
                    <h1 class="text-white font-weight-bold">추천영화</h1>
                    <hr class="divider" />
                </div>
            
            <div class="container">
                <div class="row gx-4 gx-lg-5 h-100 align-items-center justify-content-center text-center">
                <div class="col-md-6 cardImg">
                    <img src="@/assets/buzz.jpg" alt="오태식이 돌아왔구나" class="img-fluid">
                </div>
                <div class="col-md-6">
                    <h2 class="fw-bold">내가 지금부터 추천을 </h2>
                    <h2 class="mb-5 fw-bold">해줄테니 달게 받아라 </h2>
                    <h6>오태식과 병진이형이 추천해주는</h6>
                    <h6>추천영화를 받아보시고 </h6>
                    <h6>상세정보를 확인하십시오.</h6>
                </div>
                </div>
            </div>
            <router-link :to="{name: 'RandomView'}">
                <button class="w-60 btn btn-lg btn-primary" >추천영화 받으러 가기</button>
            </router-link>
                
            </div>
    </div>

        </header>
    </section>
    </div>

    
</template>

<script>

import RecentMovie from '@/components/RecentMovie.vue';
import 'swiper/dist/css/swiper.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'


export default {
    components: {
        swiper,
        swiperSlide,
        RecentMovie,
    
    },
    data() {
        return {
            isModalOpen: false,
            selectedMovie: null,
            movies: [],
            swiperOptions: {
                slidesPerView: 4,
                spaceBetween: 20,
                navigation: {
                    nextEl: '.swiper-button-next',
                    prevEl: '.swiper-button-prev',
                },
            },
        }
    },
    
    created() {
    this.$store.dispatch('getRecentMovies');
    },
    computed:{
    recentMovies(){
        return this.$store.state.recentMovies
    }
    },
    methods:{
        openModal(movie) {
            this.selectedMovie = movie;
            this.isModalOpen = true;
        },
        closeModal() {
            this.isModalOpen = false;
        }, 
    }
}


</script>
    
<style>
body{
    
    background-color: black;
}

section{
    height: 100vh;
    background: url(@/assets/sunflower.png);
}
section:before{
    content: '';
    background: linear-gradient(to top, black, transparent);
    position: absolute;
    left:0;
    height: 100%;
    width: 100%;
}
.main{
    width: 70%;
    color: whitesmoke;
    font-size: 5em;
    position: absolute;
    top:700px;
    left:50px;
    font-family: sans-serif;
}
.card1{
    width: 70%;
    color: whitesmoke;
    font-size: 5em;
    position: absolute;
    top:1000px;
    
    font-family: sans-serif;
}
<!-- .home{
    height:3500px;
} -->
header{
    width: 70%;
    color: whitesmoke;
    font-size: 5em;
    position: absolute;
    top:1100px;
    
    font-family: sans-serif;
}
.cardImg{
    width: 380px;
    height: 250px;
    margin-bottom: 20px;
}
br{
    margin-bottom: 100px;
}
.swiper-container {
    width: 100%;
    height: 400px;
}
    
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
}

.modal-content {
    background-color: whitesmoke;
    padding: 15px;
    max-width: 550px;
    max-height: 1500px;
    overflow-y: hidden;
}


.modal-title{
    margin-top: 15px;
    font-size: 1.4rem;
    
}

.overview-text{
    margin-top: 15px;
    font-size: 1rem;
    display: -webkit-box;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    margin-bottom: 20px;
}
</style>