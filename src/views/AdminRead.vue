<template>
  <div class="container">
    <h2>All the created course are listed here!</h2>
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
        <o-table-column field="code" label="課程編碼" v-slot="props">
          {{ props.row.code }}
        </o-table-column>
        <o-table-column field="category" label="體操類別" v-slot="props">
          {{ props.row.category }}
        </o-table-column>
        <o-table-column field="difficulity" label="項目難度" v-slot="props">
          {{ props.row.difficulity }}
        </o-table-column>
        <o-table-column field="coach" label="教練" v-slot="props">
          {{ props.row.code }}
        </o-table-column>

         <o-table-column label="操作" v-slot="props">
          <button>
            <router-link :to="'/adminmanage/' + props.row.id">申請人名單</router-link>
          </button>
           <button>
            <router-link :to="'/createcourse/'">更新</router-link>
          </button>
          <span>
          <button @click="deleteCourse(props.row.id)">刪除</button>
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
