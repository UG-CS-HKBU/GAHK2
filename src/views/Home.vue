<template>
  <div class="container">
    <div class="col-lg-3 centered">
      <img
        src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRba03rm_KYilCEUT_LOTYnn6DigiWthrCsvg&usqp=CAU"
      />
    </div>
    <div class="col-lg-9 jumbotron">
      <p>Welcome to GAHK Website</p>
    </div>

    <div>
      <!-- <el-table :data="list2" border style="width: 100%">
        <el-table-column type="expand">
          <template slot-scope="props">
            <el-form label-position="left" inline class="demo-table-expand">
              <el-form-item label="课程编码">
                <span>{{ props.row.code }}</span>
              </el-form-item><br>
              <el-form-item label="体操类别">
                <span>{{ props.row.category }}</span>
              </el-form-item><br>
              <el-form-item label="项目难度">
                <span>{{ props.row.difficulty }}</span>
              </el-form-item><br>
              <el-form-item label="教练">
                <span>{{ props.row.coach }}</span>
              </el-form-item><br>
              <el-form-item label="开始日期">
                <span>{{ props.row.Sdate }}</span>
              </el-form-item><br>
              <el-form-item label="结束日期">
                <span>{{ props.row.Edate }}</span>
              </el-form-item><br>
              <el-form-item label="星期">
                <span>{{ props.row.week }}</span>
              </el-form-item><br>
              <el-form-item label="上课日期">
                <span>{{ props.row.dates }}</span>
              </el-form-item><br>
              <el-form-item label="截止日期">
                <span>{{ props.row.Ddate }}</span>
              </el-form-item><br>
              <el-form-item label="年龄上限">
                <span>{{ props.row.Uage }}</span>
              </el-form-item><br>
              <el-form-item label="年龄下限">
                <span>{{ props.row.Lage }}</span>
              </el-form-item><br>
              <el-form-item label="体育馆">
                <span>{{ props.row.gym }}</span>
              </el-form-item><br>
              <el-form-item label="场地">
                <span>{{ props.row.gym1 }}</span>
              </el-form-item><br>
              <el-form-item label="名额">
                <span>{{ props.row.quato }}</span>
              </el-form-item><br>
              <el-form-item label="费用">
                <span>{{ props.row.fee }}</span>
              </el-form-item><br>
              <el-form-item label="内文">
                <span>{{ props.row.intro }}</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>

        <template>
          <el-table-column type="index" label="id" width="120"> </el-table-column>
          <el-table-column prop="code" label="活动名称" width="120"> </el-table-column>

          <el-table-column prop="code" label="操作" width="200">
             <router-link :to="'/applicationform/'+ code">去申请页面</router-link>
          </el-table-column>
        </template>
      </el-table> -->

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

        <o-table-column field="code" label="活動名稱" v-slot="props">
          {{ props.row.code }}
        </o-table-column>

        <!-- <o-table-column field="last_name" label="Last Name" v-slot="props">
          {{ props.row.last_name }}
        </o-table-column> -->

        <!-- <o-table-column
          field="date"
          label="Date"
          position="centered"
          v-slot="props"
        >
          {{ new Date(props.row.date).toLocaleDateString() }}
        </o-table-column> -->

        <o-table-column label="操作" v-slot="props">
          <button>
            <!-- <o-icon
              pack="fas"
              :icon="props.row.gender === 'Male' ? 'mars' : 'venus'"
            >
            </o-icon> -->
            <!-- {{ props.row.gender }} -->
            <router-link :to="'/applicationform/' + props.row.id">去申請頁面</router-link>
          </button>
        </o-table-column>
      </o-table>
    </div>
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
    fetch("http://localhost:1337/course/json")
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
