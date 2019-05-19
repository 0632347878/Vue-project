<template>
  <div id="app">
  <header class="header">
      <div class="container">
        <a href="/" class="logo"><img class="logo-img" src="../src/assets/images/layers.svg" alt="layers.svg"></a>
        <nav class="nav">
          <ul class="nav__list">
            <li class="nav__item"><a class="nav__action" href="#">about Us</a></li>
            <li class="nav__item"><a class="nav__action" href="#">company</a></li>
            <li class="nav__item"><a class="nav__action" href="#">careers</a></li>
            <li class="nav__item"><a class="nav__action" href="#">contacts</a></li>
          </ul>
        </nav>
        <div class="join">
          <button class="join__btn">Log In</button>      
          <button class="join__btn active">Sing UP</button>      
        </div>   
      </div>
  </header>
  <section class="main">
    <div class="container">
      <h1 class="main__title">
        Stu Unger Rise And Fall Of A Poker Genius
      </h1>
      <p class="main__subtitle">
        V7 Digital Photo Printing
      </p>
      <div class="advantages">
        <div class="advantages__item">
          <img src="../src/assets/images/clock.svg" alt="" class="advantages__item-image">
          <p class="advantages__item-description">The Skinny On Lcd
            Monitors</p>
        </div>
        <div class="advantages__item">
          <img src="../src/assets/images/star.svg" alt="" class="advantages__item-image">
          <p class="advantages__item-description">Guidelines For Inkjet
            Cartridge Refill</p>
        </div>
        <div class="advantages__item">
          <img src="./assets/images/music-player.svg" alt="" class="advantages__item-image">
          <p class="advantages__item-description">Do A Sporting Stag Do
            In Birmingham</p>
        </div>
        <div class="advantages__item">
          <img src="../src/assets/images/house.svg" alt="" class="advantages__item-image">
          <p class="advantages__item-description">Your Computer Usage </p>
        </div>
      </div>
    </div>
  </section>
  <section class="news">
    <div class="container">
      <h2 class="news__title heading2">LATEST NEWS</h2>
      <div v-if="isArticlesLoaded">Loading repositories...</div>
      <Article url="https://jsonplaceholder.typicode.com/posts"></Article>
    </div>
  </section>
  <section class="company">
    <div class="container container--lg">
      <h2 class="company__title heading2">INSIDE Company</h2>
      <div class="gallery">
        <transition name="slide-fade">
        <ul v-cloak v-if="isGalleryLoaded" class="gallery__list">
          <li v-for="item in response.data.slice(0, 50)" class="gallery__item">
            <img :src="item.thumbnailUrl" alt="" class="thumb">
            <!--<img :src="item.url" alt="" class="full">-->
          </li>
        </ul>
        </transition>
      </div>
    </div>
  </section>
  <section class="vacancies">
    <div class="container">
      <h2 class="vacancies__title heading2">HOT VACANCIES</h2>
      <ul class="vacancies__list">
        <li class="vacancies__item">
          <i class="icon-settings"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">As soon as Computerized Tomography</h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
        <li class="vacancies__item">
          <i class="icon-placeholder"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">Magnetic Resonance Imaging </h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
        <li class="vacancies__item">
          <i class="icon-shopping-cart"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">This is for the reason</h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
        <li class="vacancies__item">
          <i class="icon-like"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">After that, in the 1980s Magnetic</h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
        <li class="vacancies__item">
          <i class="icon-phone-call"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">Became accessible in the 1970s</h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
        <li class="vacancies__item">
          <i class="icon-envelope"></i>
          <div class="vacancies__info">
            <span class="vacancies__item-type">A situation</span>
            <h4 class="vacancies__item-title">MRIs concentrate on water molecules</h4>
            <p class="vacancies__item-description">No image is so essential</p>
          </div>
        </li>
      </ul>
      <div class="btn-holder">
        <button class="news__btn-more btn-more">MORE NEWS</button >
      </div>
    </div>
  </section>
  <footer class="footer">
      <div class="container">
          <div class="footer__content">
              <h2 class="footer__title heading2">Sign up for newsleter!</h2>
              <p class="footer__description">Stay informed of the last company news</p>
              <form action=""
                    class="footer__form">
                  <div class="input-holder">
                      <input class="footer__form-input"
                             type="email"
                             v-model="email"
                             placeholder="Your email">
                      <p class="error error--invalid">Invalid email</p>
                      <p class="error error--empty">Email field is required</p>
                      <p class="success">Your message has been sent</p>
                  </div>
                  <input  @click.prevent ="checkForm"
                          class="footer__form-btn"
                          type="submit"
                          value="Subscribe">
              </form>
          </div>
      </div>
  </footer>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
import Article from "./components/Article.vue";

export default {
  name: 'app',
  components: {Article},
  data() {
    return {
      email: '',
      isGalleryLoaded: false,
      response: null,
      isArticlesLoaded: false,
      galleryApi: 'https://jsonplaceholder.typicode.com/photos',
    };
  },
  methods: {
      checkForm() {
          const form = document.querySelector('.footer__form');
          if(this.email.length < 1) {
            form.classList.add('empty');
          } else if(!this.validateEmail(this.email) && (this.email.length >= 1)) {
            form.classList.add('invalid');
          } else if(this.validateEmail(this.email)) {
            form.classList.add('success');
          }
      },
       validateEmail(email) {
        const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(String(email).toLowerCase());
      }
  },
  created() {
    axios.get(this.galleryApi)
      .then((response) => {
        this.response = response;
        this.isGalleryLoaded = true;
      });
  },
  mounted() {
      const form = document.querySelector('.footer__form');
      const input = document.querySelector('.footer__form-input');
      input.addEventListener('change', function () {
          form.className = 'footer__form';
      })
  }
}
</script>

<style></style>
