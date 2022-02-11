<template>
  <div class="container">
    <h2>All the applied course are listed here!</h2>
    <div>
      <el-table :data="list" border style="width: 100%">
        <el-table-column type="index" label="id" width="120">
        </el-table-column>
        <el-table-column prop="item" label="活动项目" width="120">
        </el-table-column>
        <el-table-column prop="code" label="活动编码" width="120">
        </el-table-column>
        
        <el-table-column label="操作" width="200">
          
          <el-button type="text" >查看详情</el-button>
          <el-button type="text" size="large">取消申请</el-button>
          <el-dialog title="活动详情" :append-to-body="true">
            <el-table  :data="list">
             <el-table-column property="item" label="活动项目" width="200"></el-table-column>
             <el-table-column property="code" label="活动编码" width="200"></el-table-column>
             <el-table-column property="level" label="活动难度" width="200"></el-table-column>
            </el-table>
          </el-dialog>
         
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>

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
     return  {
      list: []
    }
  },
   mounted() {
    fetch('http://localhost:1337/student/json')
    .then(res => res.json())
    .then(data => this.list = data)
    .catch(err => console.log(err.message))
  },

  methods:{

  },
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
