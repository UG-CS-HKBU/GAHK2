<template>
  <div class="container">
    <h2>All the created course are listed here!</h2>
    <div>
     <!-- <el-table :data="list2" border style="width: 100%">
         <el-table-column type="expand">
           <template slot-scope="props">
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

        <template>
          <el-table-column type="index" label="id" width="120"> </el-table-column>
          <el-table-column prop="code" label="活动名称" width="120"> </el-table-column>

          <el-table-column slot-scope="props" label="操作" width="200">
            <el-button type="warning" size="large" @click="deleteCourse(1)">删除</el-button>
            <el-button type="text" size="large">更新</el-button>
             <el-button type="text" size="large">申请名单</el-button> 
             <router-link :to="'/adminmanage/' + props.row.id">申请人名单</router-link
            > 
          </el-table-column>
        </template>
      </el-table>   -->

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
        <o-table-column field="code" label="课程编码" v-slot="props">
          {{ props.row.code }}
        </o-table-column>
        <o-table-column field="category" label="体操类别" v-slot="props">
          {{ props.row.category }}
        </o-table-column>
        <o-table-column field="difficulity" label="项目难度" v-slot="props">
          {{ props.row.difficulity }}
        </o-table-column>
        <o-table-column field="coach" label="教练" v-slot="props">
          {{ props.row.code }}
        </o-table-column>

         <o-table-column label="操作" v-slot="props">
          <button>
            <router-link :to="'/adminmanage/' + props.row.id">申请人名单</router-link>
          </button>
           <button>
            <router-link :to="'/createcourse/' + props.row.id">更新</router-link>
          </button>
          <span>
          <button @click="deleteCourse(props.row.id)">删除</button>
          </span>
        </o-table-column>
      </o-table>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
/* eslint-disable vue/no-unused-components */
export default {
  data() {
    // let list2 = localStorage.getItem("create-course-page-data");
    // if (list2) {
    //   list2 = JSON.parse(list2);
    // }
    // return { list2: list2 || [] };

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
    fetch('http://localhost:1337/course/json')
    .then(res => res.json())
    .then(data => this.data = data)
    .catch(err => console.log(err.message))
  },

  methods: {
      async deleteCourse(id) {
        console.log(id);
        var r = confirm("Confirm Delete?");
        if (r) {
            var response = await fetch("http://localhost:1337/course/" + id, {
                method: "DELETE",
            });
            if (response.ok) {
                var html = await response.text();
                alert(html);
            } else {
                alert(response.status + ": " + response.statusText);
            }
        } else {
            alert("cancelled");
        }
    },

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
