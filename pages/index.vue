<template>
<div>
<section class="hero is-dark is-medium is-bold">
  <!-- Hero head: will stick at the top -->
  <div class="hero-head">
    <nav class="navbar">
      <div class="container">
        <div class="navbar-brand">
          <a class="navbar-item">
            <img src="https://bulma.io/images/bulma-type-white.png" alt="Logo">
          </a>
          <span class="navbar-burger burger" data-target="navbarMenuHeroA">
            <span></span>
            <span></span>
            <span></span>
          </span>
        </div>
        <div id="navbarMenuHeroA" class="navbar-menu">
          <div class="navbar-end">
            <a class="navbar-item is-active">
              Home
            </a>
            <a class="navbar-item">
              Examples
            </a>
            <a class="navbar-item">
              Documentation
            </a>
            <span class="navbar-item">
              <a class="button is-primary is-inverted">
                <span class="icon">
                  <i class="fab fa-github"></i>
                </span>
                <span>Download</span>
              </a>
            </span>
          </div>
        </div>
      </div>
    </nav>
  </div>  
</section>

<section class="section">
    <div class="container is-widescreen">
      <div class="columns is-multiline is-centered">
      <div class="columns is-vcentered">
        <div class="column is-one-quarter">
          <app-logo/>
        </div>
        <div class="column is-half text-white">
          Welcome to TheMealDB: An open, crowd-sourced database of Recipes from around the world.
          We also offer a free JSON API for anyone wanting to use it.
          If you like the site, please consider supporting us on Patreon by clicking the link below...
        </div>
        <div class="column is-one-quarter">
          <app-logo/>
        </div>
      </div>

      <div class="columns is-multiline">
      <div class="columns is-vcentered" v-for="(meal, index) in meals" :key="index">
        <div class="column is-8">
            <no-ssr  placeholder="Loading...">
             <youtube  @ready="ready" :player-vars="{ autoplay: 1 }" :video-id="meal.strYoutube" />
            </no-ssr>
        </div>
        <div class="column text-white">
          <!-- <img :src="meal.strMealThumb" :alt="meal.strMeal" width="200"> -->
          <h1 class="subtitle"> {{ meal.strMeal }} </h1><br>
          <div>{{ meal.strInstructions }}</div>
        </div>
      </div>
      </div>
      </div>
    </div>
  </section>

<section class="section">
        <div class="container">
            <div class="columns is-multiline">
                <div
                    class="column is-one-quarter"
                    v-for="(category, index) in categories"
                    :key="index">
                        <a :href="categories.url" target="_blank">
                                <div class="card-image">
                                    <figure class="image is-3by2">
                                        <img :src="category.strCategoryThumb" :alt="category.strCategory">
                                    </figure>
                                </div>
                                <div class="card-content">
                                    <div class="content">{{ category.strCategory }}</div>
                                </div>
                        </a>
                </div>
            </div>
        </div>
    </section>
</div>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'

export default {
  async asyncData({ app }) {
    const { meals } = await app.$axios.$get(
      `https://www.themealdb.com/api/json/v1/1/search.php?s=Arrabiata`
    );

    return { meals };
  },
  async asyncData({ app }) {
    const { categories } = await app.$axios.$get(
      `https://www.themealdb.com/api/json/v1/1/categories.php`
    );

    return { categories };
  },
  components: {
    AppLogo
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.text-white {
  color: white;
}
</style>

