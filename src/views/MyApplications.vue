<template>
  <div class="container">
    <h2>All the applied course are listed here!</h2>
    <div>
      <o-table
        :data="isEmpty ? [] : data"
        :bordered="isBordered"
        :striped="isStriped"
        :narrowed="isNarrowed"
        :hoverable="isHoverable"
        :loading="isLoading"
        :focusable="isFocusable"
        :mobile-cards="hasMobileCards"
      >
        <o-table-column field="id" label="ID" width="40" numeric v-slot="props">
          {{ props.row.id }}
        </o-table-column>

        <o-table-column field="code" label="活动名称" v-slot="props">
          {{ props.row.code }}
        </o-table-column>

         <o-table-column label="操作" v-slot="props">
          <span>
            <button>
             <router-link :to="'/studentdetails/'+ props.row.id">查看详情</router-link>
            </button>
            <button>取消申请</button>
          </span>
        </o-table-column>
      </o-table>

      <!-- <el-table :data="list" border style="width: 100%">
        <el-table-column type="index" label="ID" width="120">
        </el-table-column>
        <el-table-column prop="code" label="活动编码" width="120">
        </el-table-column>
        
        <el-table-column label="操作" width="200">
          
          <el-button type="text" >查看详情</el-button>
          <el-button type="text" size="large">取消申请</el-button>
          <el-dialog title="活动详情" :append-to-body="true">
            
          </el-dialog>
         
        </el-table-column>
      </el-table> -->
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
/* eslint-disable vue/no-unused-components */
export default {
  data() {
    // let list = localStorage.getItem('apply-course-page-data')
    // if (list) {
    //   list = JSON.parse(list)
    // }
    // return {
    //   list: list || [],
    //   dialogTableVisible: false,
    // };
    return {
      data: [],
      isEmpty: false,
      isBordered: false,
      isStriped: false,
      isNarrowed: false,
      isHoverable: false,
      isFocusable: false,
      isLoading: false,
      hasMobileCards: true,
    };
  },
  mounted() {
    fetch("http://localhost:1337/course/json")
      .then((res) => res.json())
      .then((data) => (this.data = data))
      .catch((err) => console.log(err.message));
  },

  methods: {},
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
