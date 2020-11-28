<template>
  <div class="resultList">
    <ul>
      <li v-for="(result, key) in resultList" :key="key">
        <a :href="result.url" class="link">{{ result.title }}</a>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType, reactive } from "vue";

export default defineComponent({
  name: "ResultList",

  props: {
    resultList: Array as PropType<string[]>,
    default: [],
  },
  setup(props, { emit }) {
    // type
    type input = string;
    type UpdateInput = () => void;
    type HandleClick = () => void;
    interface ResultList {
      id: string;
      title: string;
      updated_at: Date;
      url: string;
    }

    const resultList = computed(() => props.resultList);

    return {
      resultList,
    };
  },
});
</script>

<style scoped lang="scss">
.resultList {
  width: 400px;
  margin-top: 20px;
  border-radius: 5px;
  display: inline-block;
  background: rgb(186, 240, 219);
  padding: 20px 30px;
  a {
    font-size: 14px;
    text-decoration: none;
  }

  a:link {
    /*アクセスしたことのないリンク*/
    color: #4d4d4d;
  }

  a:visited {
    /*アクセスしたことのあるリンク*/
    color: #626262;
  }

  a:hover {
    /*マウスが上に乗っている状態*/
    color: #91a7e4;
    text-decoration: underline;
  }

  a:active {
    /*クリック中*/
    color: #e67692;
  }
  ul li {
    text-align: left;
    padding: 0px;
  }
}
</style>
