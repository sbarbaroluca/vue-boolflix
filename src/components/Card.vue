<template>
  <div class="card" @mouseover="isHover = true" @mouseleave="isHover = false">
    <transition name="fade">
    <img 
    :src="imgSrc" :alt="datas[titleKey]" v-if="!isHover" class="poster"
     />
    </transition> 
    <ul>
      <li>Titolo: {{ datas[titleKey]}}</li>
      <li v-if="datas[titleKey] != datas[originalTitleKey]">
          Titolo originale: {{ datas[originalTitleKey] }}
      </li>
      <li>
          Lingua originale:
          <span v-if="flagFinded" class="flag-container">
            <img :src="flagPath" alt="" class="flag" />
          </span>
          <div v-else class="lang-info">
              {{ langUppercase }}  
          </div>    
      </li>
      <li>
          Voto:
          <i
            v-for="i in 5"
            :key="i"
            :class="i <= finalRating ? 'fas fa-star' : 'far fa-star'">
          </i>   
      </li>
      <li v-if="datas.overview != ''">
          {{ datas.overview }}
      </li>    
    </ul>
  </div>    
</template>

<script>
export default {
      name: "Card",
      data() {
          return {
            flagFinded: false,
            flagPath: "",
            language: this.datas.original_language,
            imgPath: "https://image.tmdb.org/t/p/w342",
            isHover: false
          };
      },
      props: {
        datas: Object,
        titleKey: String,
        originalTitleKey: String
      },
      created() {
          const originalLang = this.language;
          if (originalLang == "it" || originalLang == "en") {
            if (originalLang == "it") {
                this.flagPath = require("../assets/images/it.png");
            } else if (originalLang == "en") {
                this.flagPath = require("../assets/images/en.png");
            }
            this.flagFinded = true;
          }
      },
      computed: {
        langUppercase() {
            return this.language.toUpperCase();
        },
        imgSrc() {
            let path = this.imgPath;
            if (this.datas.poster_path != null) {
                path += this.datas.poster_path;
            } else {
              if (this.datas.backdrop_path != null) {
                path += this.datas.backdrop_path;
              } else {
                  path = require("../assets/images/film.png");
              }
            }
            return path;
        },
        finalRating() {
            return Math.round(Math.round(this.datas.vote_average) / 2);
        }
      }
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
@import "~@fortawesome/fontawesame-free/css/all.css";
.card {
  position: relative;
  margin: 0 15px 30px;
  padding: 15px;
  height: 350px;
  background-color: $netflixGrey;
  color: #fff;
  img.poster {
      height: 100%;
      width: 100%;
      position: absolute;
      transform: translate(-15px, -15px);
  }
  ul {
    overflow: auto;
    li {
      margin: 5% 0;
    }
  }
  .flag {
      width: 35px;
  }
  .fas.fa-star {
    color: yellow;
  }
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
}
</style>