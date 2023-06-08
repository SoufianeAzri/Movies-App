<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://img1.ak.crunchyroll.com/i/spire4/8056a82e973dde98ebb82abd39dc69731564519729_main.jpg" alt="One Piece" class="featured-img">
        <div class="details">
          <h3>One Piece</h3>
          <p>One Piece (stylized in all caps) is a Japanese manga series written and illustrated by Eiichiro Oda. It has been serialized in Shueisha's shōnen manga magazine Weekly Shōnen Jump since July 1997, with its individual chapters compiled into 102 tankōbon volumes as of April 2022. </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" />
    </form>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/'+ movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{movie.Type}}</div>
          </div>
          <div class="detail">
            <div class="year">{{movie.Year}}</div>
            <h3>{{movie.Title}}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';
export default {
  setup(){
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = ()=>{
      if(search.value !== ""){
        fetch(`http://www.omdbapi.com/?apikey=${env.api_key}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }
    return {
      search,
      movies,
      SearchMovies
    }
  }
  
}
</script>
<style lang="scss">
  .home {
  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .details {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      h3 {
        color:#FFF;
        margin-bottom: 16px;
      }
      p {
        color: #FFF;
      }
    }
  }
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;
    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        color: #FFF;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: #f3f3f3;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42B883;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        &:active {
          background-color: #3B8070;
        }
      }
    }
  }
  .movies-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0 8px;
    .movie{
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      .movie-link{
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image{
          position: relative;
          display: block;
          img{
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          .type{
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #fff;
            text-transform: capitalize;
            bottom: 16px;
            left: 0;
          }
        }
        .detail{
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0 0 8px 8px;
          .year{
            color: #AAA;
            font-size: 14px;
          }
          h3{
            font-weight: 600;
            color: #fff;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>