<template>
  <div class="max-w-screen-2xl px-10 mx-auto py-10">
    <div class="text-2xl mb-4">Psychologists available</div>
    <div class="flex flex-wrap gap-5 items-center mb-10">
      <div class="w-56">
        <SelectBox
          :options="types"
          :default="typeVal"
          icon="/assets/icons/users.svg"
          @input="filterData('type', $event)"
        />
      </div>
      <div class="w-56">
        <SelectBox
          :options="[]"
          default="Speciality"
          icon="/assets/icons/adress-book.svg"
          @input="filterData('speciality', $event)"
        />
      </div>
      <div class="w-56">
        <SelectBox
          :options="['man', 'women']"
          :default="gender"
          icon="/assets/icons/man-woman.svg"
          @input="filterData('gender', $event)"
        />
      </div>
      <div class="w-56">
        <SelectBox
          :options="['en', 'ukr']"
          :default="language"
          icon="/assets/icons/language.svg"
          @input="filterData('language', $event)"
        />
      </div>
      <div class="w-56">
        <Input
          icon="/assets/icons/search.svg"
          placeholder="Name"
          :default="name"
          v-on:change="(event) => filterData('name', event.target.value)"
        />
      </div>
      <div>
        <button class="flex gap-2" @click="clearFilter">
          <img src="~/assets/icons/x.svg" alt="" />
          Clear
        </button>
      </div>
    </div>

    <div class="grid md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
      <div v-for="item in items" class="mx-auto">
        <div class="w-full max-w-sm bg-white border border-gray-200 rounded-lg shadow">
          <div class="flex flex-col items-center p-10">
            <img
              class="w-24 h-24 mb-3 rounded-full shadow-lg"
              :src="item.photo"
              alt="Bonnie image"
            />
            <h5 class="mb-1 text-xl font-medium text-gray-900">{{ item.name }}</h5>
            <span class="text-sm text-gray-500 text-center">
              {{ types[item.type] }} Clinical Psychologists</span
            >
            <div class="text-sm text-center mt-3 opacity-80">
              {{ item.note }}
            </div>
            <div class="mt-3 text-sm opacity-80">Next sessions on Monday 9th Nov</div>
            <div class="flex flex-wrap justify-around gap-1 mt-2">
              <button
                class="w-20 py-1 text-sm text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800"
              >
                8am(+$25)
              </button>
              <button
                class="w-20 py-1 text-sm text-center text-gray-900 bg-white border border-gray-300 rounded-lg hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-700 dark:focus:ring-gray-700"
              >
                9am
              </button>
              <button
                class="w-20 py-1 text-sm text-center text-gray-900 bg-white border border-gray-300 rounded-lg hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-700 dark:focus:ring-gray-700"
              >
                10am
              </button>
              <button
                class="w-20 py-1 text-sm text-center text-gray-900 bg-white border border-gray-300 rounded-lg hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-700 dark:focus:ring-gray-700"
              >
                11.30am
              </button>
              <button
                class="w-20 py-1 text-sm text-center text-gray-900 bg-white border border-gray-300 rounded-lg hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-700 dark:focus:ring-gray-700"
              >
                12.30am
              </button>
              <div class="w-full flex justify-center">
                <button class="text-[12px] underline">See More...</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import psychologists from "~/static/fakeData/psychologists";
import staticTypes from "~/static/fakeData/types";

export default {
  data() {
    return {
      items: psychologists,
      types: staticTypes,

      typeVal: "Type",
      gender: "Gender",
      language: "Language",
      name: "",
    };
  },
  mounted() {
    // console.log(types);
  },
  methods: {
    filterData(key, value) {
      if (key === "type") this.typeVal = value;
      if (key === "gender") this.gender = value;
      if (key === "language") this.language = value;
      if (key === "name") this.name = value;

      let filteredData = [...psychologists];
      if (this.typeVal !== "Type")
        filteredData = filteredData.filter(
          (item) => item.type == staticTypes.indexOf(this.typeVal)
        );
      if (this.gender !== "Gender")
        filteredData = filteredData.filter(
          (item) => item.gender.indexOf(this.gender) > -1
        );
      if (this.language !== "Language")
        filteredData = filteredData.filter(
          (item) => item.language.indexOf(this.language) > -1
        );
      if (this.name !== "")
        filteredData = filteredData.filter((item) => item.name.indexOf(this.name) > -1);

      this.items = filteredData;
    },

    clearFilter() {
      this.typeVal = "Type";
      this.gender = "Gender";
      this.language = "Language";
      this.name = "";
      this.items = psychologists;
    },
  },
};
</script>
