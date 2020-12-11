<template>
  <section class="w-full flex-none -ml-full ">
    <div class="box pt-6">
      <div class="box-wrapper p-4">
        <div class=" rounded flex items-center w-full p-3 shadow-sm border border-gray-200">
          <button
            @click="$router.push({ path: 'wallpaper', query: { key: SearchData,s:ServerType,d:DateType,i:ImageType } })"
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
            @keydown.enter="$router.push({ path: 'wallpaper', query: { key: SearchData,s:ServerType,d:DateType,i:ImageType } })"
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
    </div>
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
              :src="item.url"
              :alt="item.url"
              onerror="this.style.display='none';"
              class="rounded-md lazy"
            />
          </stack-item>
        </stack>
      </client-only>

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
    let number = Math.floor(Math.random() * 8);
    let ListImage = [
      "Naruto",
      "Black Clover",
      "mob psycho",
      "demon slayer",
      "fireforce",
      "seven deadly sins",
      "My hero Academia",
      "one punch",
    ];
    const urlData = await $axios.$get(
      `api/ser/y/"${ListImage[number]}" "wallpaper"`
    );
    return {
      urlData,
    };
  },
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
