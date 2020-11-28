<template>
  <div class="SearchArticle">
    <div class="title">Qiita 検索</div>
    <Form
      v-model:input="state.keyword"
      inputCaption="Keyword"
      buttonCaption="Search"
      @button-click="SearchApi"
      @update-input="UpdateInput"
    />
    <ResultList :result-list="state.resultList"></ResultList>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType, ref, reactive } from "vue";
import Form from "@/components/Form.vue";
import ResultList from "@/components/ResultList.vue";
import { createLogger } from "vuex";
import axios from "axios";

export default defineComponent({
  name: "SearchArticle",
  components: {
    Form,
    ResultList,
  },
  setup(props, { emit }) {
    // type
    type keyword = string;
    type HandleClick = () => void;
    interface Result {
      id: string;
      title: string;
      updatedAt: string;
      url: string;
    }

    const state = reactive<{ keyword: string; resultList: Result[] }>({
      keyword: "",
      resultList: [],
    });

    const SearchApi = () => {
      axios
        .get("https://qiita.com/api/v2/items?query=body:" + state.keyword)
        .then((response) => {
          state.resultList = [];
          response.data.forEach((el: Result) => {
            const obj = {
              id: el.id,
              title: el.title,
              updatedAt: el.updatedAt,
              url: el.url,
            };
            state.resultList.push(obj);
          });
        })
        .catch((e) => {
          console.log(e);
        });
    };

    const UpdateInput = (val: string) => {
      state.keyword = val;
    };

    return {
      state,
      SearchApi,
      UpdateInput,
    };
  },
});
</script>

<style scoped lang="scss">
.title {
  position: relative;
  left: -180px;
  color: rgb(141, 224, 192);
  font-weight: bold;
}
</style>
