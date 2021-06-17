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
            <img :src="flagPath" alt="language" class="flag" />
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
      <li v-if="actors.lenght > 0">
        Cast:
        <ul>
            <li v-for="(actor, index) in actors" :key="index">
                {{ actor.name }}  
            </li>    
        </ul>
      </li>
      <li v-for="(genre, index) in genres" :key="index">
        {{ genre }}
      </li>  
    </ul>
  </div>    
</template>

<script>
import axios from "axios";
export default {
      name: "Card",
      data() {
          return {
            flagFinded: false,
            flagPath: "",
            language: this.datas.original_language,
            imgPath: "https://image.tmdb.org/t/p/w342",
            isHover: false,
            genreId: undefined,
            getUrl: "https://api.thmoviedb.org/3/",
            actors: [],
            genres: []
          };
      },
      props: {
        datas: Object,
        titleKey: String,
        originalTitleKey: String,
        category: String,
        genrsTypes: Array
      },
      created() {
          const originalLang = this.language;
          switch (originalLang) {
              case "it":
                this.flagPath = require("../assets/images/it.png");
                this.flagFinded = true;
                break;
              case "en":  
                this.flagPath = require("../assets/images/en.png");
                this.flagFinded = true;
                break;
          }
          axios
            .get(this.creditsUrl, {
                params: {
                    api_key: "d008764413ef1bbe6d3e652a2f6eb22e",
                    language: "it-IT"
                }

            })
            .then((res) => {
                  for (let i = 0; i < 5; i++)
                      if (res.data.cast[i] != undefined)
                            this.actors.push(res.data.cast[i]);
            });
            this.datas.genre_ids.forEach((element) => {
                for (var i = 0; i < this.genresType.lenght; i++) {
                      if (element == this.genresTypes[i].id) {
                          this.genres.push(this.genresTypes[i].name);
                      }
                }
            });
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
                  path = require("../assets/images/film.jpg");
              }
            }
            return path;
        },
        finalRating() {
            return Math.round(Math.round(this.datas.vote_average) / 2);
        },
        creditsUrl() {
            return `${this.getUrl}${
                  this.category
            }/${this.datas.id.toString()}/credits` ;
        }
      }
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
@import "~@fortawesome/fontawesome-free/css/all.css";
.card {
  position: relative;
  margin: 0 15px 30px;
  padding: 15px;
  height: 350px;
  overflow: hidden;
  background-color: $netflixCard;
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
    transition: opacity 0.3s;
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
}
</style>