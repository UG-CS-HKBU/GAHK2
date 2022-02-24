<template>
  <div class="container">
  <h2>Here shows the details of the course</h2>
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
      <o-table-column field="difficulty" label="項目難度" v-slot="props">
        {{ props.row.difficulty }}
      </o-table-column>
      <o-table-column field="coach" label="教練" v-slot="props">
        {{ props.row.code }}
      </o-table-column>
    </o-table>
    

    <!-- <div>
      <el-table :data="list2" border style="width: 100%">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="課程編碼">
              <span>{{ props.row.code }}</span> </el-form-item
            ><br />
            <el-form-item label="體操類別">
              <span>{{ props.row.category }}</span> </el-form-item
            ><br />
            <el-form-item label="項目難度">
              <span>{{ props.row.difficulty }}</span> </el-form-item
            ><br />
            <el-form-item label="教練">
              <span>{{ props.row.coach }}</span> </el-form-item
            ><br />
            <el-form-item label="開始日期">
              <span>{{ props.row.Sdate }}</span> </el-form-item
            ><br />
            <el-form-item label="結束日期">
              <span>{{ props.row.Edate }}</span> </el-form-item
            ><br />
            <el-form-item label="星期">
              <span>{{ props.row.week }}</span> </el-form-item
            ><br />
            <el-form-item label="上課日期">
              <span>{{ props.row.dates }}</span> </el-form-item
            ><br />
            <el-form-item label="截止日期">
              <span>{{ props.row.Ddate }}</span> </el-form-item
            ><br />
            <el-form-item label="年齡上限">
              <span>{{ props.row.Uage }}</span> </el-form-item
            ><br />
            <el-form-item label="年齡下限">
              <span>{{ props.row.Lage }}</span> </el-form-item
            ><br />
            <el-form-item label="體育館">
              <span>{{ props.row.gym }}</span> </el-form-item
            ><br />
            <el-form-item label="場地">
              <span>{{ props.row.gym1 }}</span> </el-form-item
            ><br />
            <el-form-item label="名額">
              <span>{{ props.row.quato }}</span> </el-form-item
            ><br />
            <el-form-item label="費用">
              <span>{{ props.row.fee }}</span> </el-form-item
            ><br />
            <el-form-item label="内文">
              <span>{{ props.row.intro }}</span>
            </el-form-item>
          </el-form>
        </template>
      </el-table>
    </div> -->
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
export default {
  data() {
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
    fetch("http://localhost:1337/course/read/" + this.$route.params.id)
      .then((res) => res.json())
      .then((data) => (this.data = data))
      .catch((err) => console.log(err.message));
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
