<template>
  <transition name="slide-fade">
    <div v-if="loaded">
      <ul class="news__list">
        <li class="news__item show" :key="item.id" :data-user-id="item.userId" :data-id="item.id" v-for="item in response.data">
          <div class="news__item-preview">
            <img :src=" 'https://picsum.photos/id/' + item.id + '/432/288' "
                 ref="image"
                 @error="imgFallback()"
                 alt="no Image">
          </div>
          <div class="news__item-content">
            <h3 class="news__item-title">{{ item.title }}</h3>
            <p class="news__item-description">{{ item.body }}</p>
            <a href="#" class="news__item-more">Read me</a>
          </div>
        </li>
      </ul>
      <div class="btn-holder">
        <button @click="showItemsEvent()"
                class="news__btn-more btn-more">MORE NEWS</button>
      </div>
    </div>
  </transition>
</template>

<script>
  import axios from 'axios';
  import $  from 'jquery';

export default {
  name: 'Article',
  props: ['url']
  ,
  data() {
    return {
      loaded: false,
      response: null,
      flag: false,
      fallbackImg: 'https://picsum.photos/id/237/432/288'
    }
  },
  methods: {
    imgFallback: function () {
      const _self = this;
      if (!this.flag && this.loaded) {
        this.$refs.image.forEach(function (ref) {
          if (ref.width < 200) {
            ref.setAttribute('src', _self.fallbackImg);
          }
        });
        this.isLoaded();

        return this.flag = true;
      }
    },
    isLoaded: function () {
      this.$root.isArticlesLoaded = this.loaded;
    },

    showItemsEvent: function() {
      this.showItems(6);
    },

    showItems: function (itemsCount) {
      var $this = $(this),
              ul = $('.news__list'),
              showButton = $('.news__btn-more'),
              hidden = ul.find('li.show:hidden');

      hidden.addClass('invisible');
      ul.find('li.show:hidden:lt(' + itemsCount + ')').show("slow");
      if (hidden.length <= 4) {
        showButton.css('display', 'none');
      }
      if (!hidden.length) {
        ul.find('li.invisible').hide();
        $this.removeClass('disabled');
      }
    }
  },

  created() {
    this.showItems(6);
    axios.get(this.url)
      .then((response) => {
        this.response = response;
        this.loaded = true;
      });
  }
}
</script>

<style></style>