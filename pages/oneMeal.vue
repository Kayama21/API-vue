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
            
              <nuxt-link to="/" class="navbar-item"> Home </nuxt-link>
            
            <a class="navbar-item is-active">
              One Meal
            </a>
            <a class="navbar-item" href="https://www.themealdb.com/api.php">
              List API
            </a>
            <span class="navbar-item">
              <a class="button is-primary is-inverted" href="https://github.com/Kayama21/API-vue">
                <span class="icon">
                  <i class="fab fa-github"></i>
                </span>
                <span>Git Repository</span>
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
                <div class="columns is-multiline" v-for="(meal, oneMeal) in meals" :key="oneMeal">
                    <div class="columns is-vcentered">
                        <div class="column is-8">
                            <no-ssr  placeholder="Loading...">
                                <youtube  @ready="ready" :player-vars="{ autoplay: 1 }" :video-id="meal.strYoutube" />
                            </no-ssr>
                        </div>
                        <div class="column text-white">
                            <h1 class="subtitle"> {{ meal.strMeal }} </h1><br>
                            <h1 class="text-white-big"> What is?  </h1><br>
                            <div>Spicy Arrabiata Penne.  Doesn’t it look totally delish?  
                                This spicy pasta recipe from Valerie’s Home Cooking: 
                                More than 100 Delicious Recipes to Share with Friends and Family 
                                is a simple yet flavorful dish that’s perfect for weeknight meals as well as for entertaining.
                                originally from Italia, so for you fans of italian food this is what your looking for.</div>
                        </div>
                    </div>
                    <div class="columns is-vcentered">
                        <div class="column is-3 is-centered text-white" style="overflow-x:auto;">
                            <h1 class="text-white-big"> Ingredient : </h1><br>
                            <tr>
                                <th>Ingredient</th>
                                <th>Measurement</th>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient1 }}</td>
                                <td>{{ meal.strMeasure1 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient2 }}</td>
                                <td>{{ meal.strMeasure2 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient3 }}</td>
                                <td>{{ meal.strMeasure3 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient4 }}</td>
                                <td>{{ meal.strMeasure4 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient5 }}</td>
                                <td>{{ meal.strMeasure5 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient6 }}</td>
                                <td>{{ meal.strMeasure6 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient7 }}</td>
                                <td>{{ meal.strMeasure7 }}</td>
                            </tr>
                            <tr>
                                <td>{{ meal.strIngredient8 }}</td>
                                <td>{{ meal.strMeasure8 }}</td>
                            </tr>
                        </div>
                        <div class="column text-white">
                            <h1 class="text-white-big"> How to make : </h1><br>
                            <div>{{ meal.strInstructions }}</div>
                        </div>
                    </div>
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

.text-white-big {
  color: white;
  font-size: 25px;
}
th, td {
  text-align: left;
  padding: 8px;
}
table {
  border-collapse: collapse;
  width: 100%;
}
</style>

