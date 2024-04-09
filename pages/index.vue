<template>
  <section
    class="relative mt-4 rounded-xl overflow-hidden min-h-[500px] flex items-center"
  >
    <img
      src="~/assets/images/hero.jpg"
      alt=""
      class="absolute h-full w-full object-cover"
    />
    <div class="bg-[#262522]/60 absolute inset-0"></div>
    <div
      class="relative flex flex-col items-center justify-center w-full z-10 text-center text-white"
    >
      <h1 class="text-4xl md:text-6xl max-w-[800px] uppercase font-bold">
        Unleash Culinary Excellence
      </h1>
      <div class="max-w-[430px] mt-2 px-4">
        Explore a world of flavors, discover handcrafted recipes, and let the
        aroma of our passion for cooking fill your kitchen
      </div>
      <button
        class="text-gray-900 bg-orange-400 h-8 px-6 rounded-full uppercase font-bold mt-4"
      >
        explore recipes
      </button>
    </div>
  </section>

  <section class="mt-4 p-4 bg-blue-200 rounded-2xl">
    <div class="flex flex-wrap items-end">
      <div class="grow">
        <button
          class="text-white bg-primary h-8 px-6 rounded-full uppercase font-bold mt-4"
        >
          explore
        </button>
        <h2 class="text-4xl font-bold uppercase max-w-96 my-4">
          Our diverse Palette
        </h2>
        <div class="text-gray-600 max-w-lg">
          If you are a breakfast enthusiast, a connoisseur of savory delights,
          or on the lookout for irresistible desserts, our curated selection has
          something to satisfy every palate.
        </div>
        <button
          class="mt-6 uppercase border border-gray-900 h-8 px-4 rounded-full font-bold"
        >
          see more
        </button>
      </div>
      <div class="grow">
        <div
          class="p-4 flex justify-between items-center border-b border-gray-400 w-full uppercase text-lg"
        >
          <img src="~/assets/images/breakfest.svg" alt="" />
          <span>Breakfest</span>
        </div>
        <div
          class="p-4 flex justify-between items-center border-b border-gray-400 w-full uppercase text-lg"
        >
          <img src="~/assets/images/lunch.svg" alt="" />
          <span>Lunch</span>
        </div>
        <div
          class="p-4 flex justify-between items-center border-b border-gray-400 w-full uppercase text-lg"
        >
          <img src="~/assets/images/dinner.svg" alt="" />
          <span>Dinner</span>
        </div>
        <div
          class="p-4 flex justify-between items-center border-b border-gray-400 w-full uppercase text-lg"
        >
          <img src="~/assets/images/dessert.svg" alt="" />
          <span>Dessert</span>
        </div>
        <div
          class="p-4 flex justify-between items-center border-b border-gray-400 w-full uppercase text-lg"
        >
          <img src="~/assets/images/bite.svg" alt="" />
          <span>Quick bite!</span>
        </div>
      </div>
    </div>
  </section>

  <section class="mt-4 p-4 border border-gray-900 rounded-2xl">
    <div class="flex justify-between mb-6">
      <h2 class="text-4xl font-bold uppercase">featured recipes</h2>
      <div class="flex gap-2">
        <button class="w-8 h-8 border border-gray-900 opacity-50 rounded-full">
          <i class="fa fa-chevron-left" aria-hidden="true"></i>
        </button>
        <button class="w-8 h-8 border border-gray-900 rounded-full">
          <i class="fa fa-chevron-right" aria-hidden="true"></i>
        </button>
      </div>
    </div>
    <div class="flex overflow-x-auto overscroll-auto gap-4 pb-4">
      <Card
        v-for="meal in features"
        :key="meal.idMeal"
        size="w-full max-w-[40%]"
        :image="meal.strMealThumb"
        :title="meal.strMeal"
        :description="meal.strInstructions"
        :category="meal.strCategory"
        :area="meal.strArea"
      />
    </div>
  </section>

  <section class="pt-12" v-if="meals.length > 0">
    <div class="mx-auto max-w-md my-6 text-center">
      <div
        class="bg-primary text-white px-2 py-1 rounded-full inline uppercase"
      >
        Recipes
      </div>
      <h2 class="my-2 text-4xl uppercase font-bold">Embark on a journey</h2>
      <div>
        With our diverse collection of recipes we have something to satisfy
        every palate.
      </div>
    </div>
    <div
      class="flex flex-wrap justify-center mb-12 uppercase gap-4 font-medium"
    >
      <button
        v-for="category in categories"
        :key="category"
        class="px-4 border border-gray-900 rounded-full opacity-50 hover:opacity-100"
        :class="category_selected === category ? 'bg-lime-500 opacity-100' : ''"
        @click="changeCategory(category)"
      >
        {{ category }}
      </button>
    </div>
    <div class="flex flex-wrap gap-4">
      <template v-for="(meal, i) in meals">
        <Card
          size="w-full md:w-[32%]"
          v-if="i < limit"
          :key="meal.idMeal"
          :image="meal.strMealThumb"
          :title="meal.strMeal"
          :category="meal.strCategory"
        />
      </template>
    </div>
    <div class="flex justify-center py-12">
        <button class="text-white bg-gray-900 h-8 px-6 rounded-full uppercase" v-if="meals.length > limit" @click="loadMore(meals.length)">load more</button>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      category_selected: "All",
      meals: [],
      allmeals: [],
      categories: ["All", "Vegan", "Breakfast", "Seafood", "Beef", "Dessert"],
      features: [],
      limit: 6,
    };
  },
  async mounted() {
    const { meals: features } = await $fetch(
      "https://www.themealdb.com/api/json/v1/1/search.php?f=a"
    );
    this.features = features;
    await this.getByCategory("Vegan", this.allmeals);
    await this.getByCategory("Breakfast", this.allmeals);
    await this.getByCategory("Seafood", this.allmeals);
    await this.getByCategory("Beef", this.allmeals);
    await this.getByCategory("Dessert", this.allmeals);
    this.meals = this.allmeals;
  },
  methods: {
    async getByCategory(category, array) {
      const { meals: data } = await $fetch(
        "https://www.themealdb.com/api/json/v1/1/filter.php?c=" + category
      );

      for (var i = 0; i < 3; i++) {
        if (data[i]) {
          data[i].strCategory = category;
          array.push({ ...data[i] });
        }
      }
    },
    changeCategory(category) {
      this.category_selected = category;
      let data = JSON.parse(JSON.stringify(this.allmeals));
      if (category === "All") {
        this.meals = data;
        return;
      }
      this.meals = data.filter((e) => e.strCategory === category);
    },
    loadMore(limit) {
        this.limit = limit
    }
  },
};
</script>