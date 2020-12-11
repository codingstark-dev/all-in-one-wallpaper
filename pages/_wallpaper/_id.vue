<template>
  <section class="w-full flex-none -ml-full ">

    <!-- <div class="box pt-6">
      <div class="box-wrapper p-4">
        <div class=" rounded flex items-center w-full p-3 shadow-sm border border-gray-200">
          <button
            @click="$router.push({ path: '/wallpaper', query: { key: SearchData,s:ServerType,d:DateType,i:ImageType } })"
            class="outline-none focus:outline-none"
          ><svg
              class=" w-5 text-gray-600 h-5 cursor-pointer"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
            </svg></button>
          <input
            type="search"
            name=""
            id=""
            autocomplete="on"
            @keydown.enter="refreshPage"
            placeholder="Search Wallpaper Here"
            v-model="SearchData"
            class="w-full pl-4 text-sm outline-none  focus:outline-none bg-transparents"
          >
          <div class="select">
            <select
              v-model="DateType"
              class="text-sm w-12  outline-none focus:outline-none bg-transparent"
            >
              <option value="Day">Day</option>
              <option value="Month">Month</option>
              <option
                value="Year"
                selected
              >Year</option>
            </select>
          </div>
          <div class="select">
            <select
              v-model="ServerType"
              class="text-sm w-12 outline-none focus:outline-none bg-transparent"
            >
              <option
                value="All"
                selected
              >All</option>
              <option value="Reddit">Reddit</option>
              <option value="Wallpapercave">Wallpapercave</option>
            </select>
          </div>
          <div class="select">
            <select
              v-model="ImageType"
              class="text-sm w-12  outline-none focus:outline-none bg-transparent"
            >
              <option
                value="hd wallpaper"
                selected
              >Hd</option>
              <option value="4k wallpaper">4k</option>
              <option value="Desktop wallpaper">Desktop</option>
            </select>
          </div>
        </div>

      </div>
    </div> -->
    <div
      v-if="urlData !== null && urlData !== undefined"
      class="p-10"
    >
      <client-only>
        <stack
          :column-min-width="130"
          :gutter-width="15"
          :gutter-height="15"
          monitor-images-loaded
        >
          <stack-item
            v-for="(item, i) in urlData['results']"
            :key="i"
            style="transition: transform 200ms"
          >
            <img
              id="imageI"
              :src='item.url'
              :alt="item.url"
              onerror="this.style.display='none';"
              class="rounded-md "
            />
          </stack-item>
        </stack>
      </client-only>
      <!-- <div v-for="item in datas['results']" :key="item.url">
            <h1>{{item.url}}</h1>
        </div>
    -->
    </div>

  </section>
</template>

<script>
export default {
  data() {
    return {
      DateType: "Year",
      ServerType: "All",
      ImageType: "hd wallpaper",
      SearchData: null,
    };
  },

  async asyncData({
    $axios,
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error,
  }) {
    if (query.s == "Reddit" || query.s == "Wallpapercave") {
      const urlData = await $axios.$get(
        `api/ser/${query.d}/site:${query.s}.com ${query.key} "${query.i}"`
      );

      return {
        urlData,
        DateType: query.d,
        ServerType: query.s,
        ImageType: query.i,
        SearchData: query.key,
      };
    } else {
      const urlData = await $axios.$get(
        `api/ser/${query.d}/${query.key} "${query.i}"`
      );

      return {
        urlData,
      };
    }
  },
};
</script>

<style lang="scss" scoped>
</style>