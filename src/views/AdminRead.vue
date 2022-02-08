<template>
  <div class="container">
    <h2>All the created course are listed here!</h2>
    <div>
      <el-table :data="list2" border style="width: 100%">
        <el-table-column type="expand">
          <template>
            <el-form label-position="left" inline class="demo-table-expand">
              <el-form-item label="课程编码">
                <span>{{ props.row.code }}</span>
              </el-form-item>
              <el-form-item label="体操类别">
                <span>{{ props.row.category }}</span>
              </el-form-item>
              <el-form-item label="项目难度">
                <span>{{ props.row.difficulty }}</span>
              </el-form-item>
              <el-form-item label="教练">
                <span>{{ props.row.coach }}</span>
              </el-form-item>
              <el-form-item label="开始日期">
                <span>{{ props.row.Sdate }}</span>
              </el-form-item>
              <el-form-item label="结束日期">
                <span>{{ props.row.Edate }}</span>
              </el-form-item>
              <el-form-item label="星期">
                <span>{{ props.row.week }}</span>
              </el-form-item>
              <el-form-item label="上课日期">
                <span>{{ props.row.dates }}</span>
              </el-form-item>
              <el-form-item label="截止日期">
                <span>{{ props.row.Ddate }}</span>
              </el-form-item>
              <el-form-item label="年龄上限">
                <span>{{ props.row.Uage }}</span>
              </el-form-item>
              <el-form-item label="年龄下限">
                <span>{{ props.row.Lage }}</span>
              </el-form-item>
              <el-form-item label="体育馆">
                <span>{{ props.row.gym }}</span>
              </el-form-item>
              <el-form-item label="场地">
                <span>{{ props.row.gym1 }}</span>
              </el-form-item>
              <el-form-item label="名额">
                <span>{{ props.row.quato }}</span>
              </el-form-item>
              <el-form-item label="费用">
                <span>{{ props.row.fee }}</span>
              </el-form-item>
              <el-form-item label="内文">
                <span>{{ props.row.intro }}</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>

        <template slot-scope="scope">
          <el-table-column type="index" label="id" width="120"> </el-table-column>
          <el-table-column prop="code" label="活动名称" width="120"> </el-table-column>

          <el-table-column label="操作" width="200">
            <el-button @click="list2.splice(scope.$index, 1)" type="warning" size="large"
              >删除</el-button
            >
            <el-button type="text" size="large">更新</el-button>
          </el-table-column>
        </template>
      </el-table>
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/no-unused-components */
export default {
  data() {
    let list2 = localStorage.getItem("create-course-page-data");

    if (list2) {
      list2 = JSON.parse(list2);
    }

    return { list2: list2 || [] };

    // return  {
    //   info: []
    // }
  },

  // mounted() {
  //   fetch('http://localhost:8080/CreateCourse')
  //   .then(res => res.json())
  //   .then(data => this.info = data)
  //   .catch(err => console.log(err.message))
  // },

  methods: {
    // handleDelete(index, row) {
    // this.$confirm("此操作将删除该课程所有信息, 是否继续?", "提示", {
    //   cancelButtonText: "取消",
    //   confirmButtonText: "确定",
    //   type: "warning"
    // })
    //   .then(() => {
    //     this.axios
    //       .get("http://localhost:8080/AdminRead/Delete?id=" + row.Id)
    //       .then(result => {
    //         if (result.status == 200 || result.status == 302) {
    //           this.$message({
    //             message: "删除成功",
    //             type: "success"
    //           });
    //           this.getAllcourses();
    //         }
    //       })
    //       .catch(err => { // eslint-disable-line no-unused-vars
    //         this.$message({
    //           message: "删除失败",
    //           type: "danger"
    //         });
    //       });
    //   })
    //   .catch(() => {
    //     this.$message({
    //       type: "info",
    //       message: "已取消删除"
    //     });
    //   });
    // },
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
,
.demo-table-expand {
  font-size: 0;
}
.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}
.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}
</style>
