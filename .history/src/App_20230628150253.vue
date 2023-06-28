<template>
  <el-config-provider :locale="elLocale">
    <div id="app">
      <VFormDesigner
        ref="vfDesignerRef"
       
        :web-config="webConfig"
        :global-dsv="globalDsv"
      >
        <!--
      <template #customToolButtons>
        <el-button type="text" @click="doTest">测试btn</el-button>
      </template>
      -->
      </VFormDesigner>
    </div>
  </el-config-provider>
</template>

<script>
import VFormDesigner from "./components/form-designer/index.vue";

import zhCNLang from "element-plus/lib/locale/lang/zh-cn";
import enUSLang from "element-plus/lib/locale/lang/en";
import { nextTick } from "vue";

export default {
  name: "App",
  components: {
    VFormDesigner,
  },
  data() {
    return {
      elLocaleMap: {
        "zh-CN": zhCNLang,
        "en-US": enUSLang,
      },

      //全局数据源变量
      globalDsv: {
        testApiHost: "http://www.test.com/api",
        testPort: 8080,
      },
      webConfig: {
        BEAUTIFIER_PATH_CUS: "",
        ACE_BASE_PATH_CUS: "",
      },
    };
  },
  computed: {
    elLocale() {
      let curLocale = localStorage.getItem("v_form_locale") || "zh-CN";
      return this.elLocaleMap[curLocale];
    },
  },
  created() {
    nextTick(() => {
      this.$refs.vfDesignerRef.setFormConfig({
        name: "123",
        nameDisabled:true,
        code: "456",
        codeDisabled:true,
        category: "测试",
      });
      this.$refs.vfDesignerRef.setCategory([
        {
          id: 1,
          parentId: -1,
          children: [
            {
              id: 3,
              parentId: 1,
              children: [],
              name: "请假",
              code: "12",
              sort: 6,
              createTime: "2023-05-30 15:51:11",
              updateTime: "2023-05-30 16:45:38",
            },
            {
              id: 8,
              parentId: 1,
              children: [],
              name: "用车",
              code: "car",
              sort: 0,
              createTime: "2023-06-16 10:43:34",
            },
          ],
          name: "行政管理",
          code: "1",
          sort: 0,
          createTime: "2023-05-30 15:50:20",
          updateTime: "2023-05-30 16:31:23",
        },
        {
          id: 2,
          parentId: -1,
          children: [
            {
              id: 4,
              parentId: 2,
              children: [],
              name: "合同盖章",
              code: "234",
              sort: 0,
              createTime: "2023-05-30 16:00:53",
              updateTime: "2023-05-30 17:03:55",
            },
          ],
          name: "合同管理",
          code: "2",
          sort: 0,
          createTime: "2023-05-30 15:50:34",
          updateTime: "2023-05-30 16:31:28",
        },
        {
          id: 5,
          parentId: -1,
          children: [
            {
              id: 7,
              parentId: 5,
              children: [],
              name: "测试1",
              code: "987",
              sort: 5,
              createTime: "2023-05-30 17:28:05",
            },
            {
              id: 6,
              parentId: 5,
              children: [],
              name: "测试",
              code: "9991",
              sort: 0,
              createTime: "2023-05-30 17:07:05",
              updateTime: "2023-05-30 17:12:00",
            },
          ],
          name: "测试类别",
          code: "999",
          remark: "",
          sort: 0,
          createTime: "2023-05-30 17:06:31",
          updateTime: "2023-05-30 17:17:18",
        },
      ]);
    });
  },
  methods: {
    doTest() {
      let fieldList = this.$refs.vfDesignerRef.getFieldWidgets(null, true);
      console.log("test", fieldList);
    },
  },
};
</script>

<style lang="scss">
#app {
  height: 100%;
}
</style>
