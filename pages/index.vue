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
            
              <nuxt-link to="/oneMeal" class="navbar-item"> One Meal </nuxt-link>
            
            <a class="navbar-item" href="https://www.themealdb.com/api.php">
              List API
            </a>
            <span class="navbar-item">
              <a class="button is-primary is-inverted" href="https://github.com/Kayama21/API-vue">
                <span class="icon">
                  <i class="fab fa-github"></i>
                </span>
                <span>Git Repsitory</span>
              </a>
            </span>
          </div>
        </div>
      </div>
    </nav>
  </div>  
</section>

    <div class="hero-body">
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
    </div>

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

