<template>
<h2>{{ applicantInfo }}</h2>
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
      </o-table>
</div>

<!-- <div>
      <el-table :data="list3" border style="width: 100%">
        <el-table-column type="index" label="id" width="80">
        </el-table-column>
        <el-table-column prop="item" label="活动项目" width="120">
        </el-table-column>
        <el-table-column prop="code" label="活动编码" width="120">
        </el-table-column>
         <el-table-column prop="level" label="难度" width="120">
        </el-table-column>
         <el-table-column prop="Ename" label="紧急联系人姓名" width="120">
        </el-table-column>
        <el-table-column prop="tel" label="紧急联系人电话" width="120">
        </el-table-column>
        <el-table-column prop="address" label="住址" width="120">
        </el-table-column>
        <el-table-column prop="paying" label="付款方式" width="120">
        </el-table-column>
        <el-table-column prop="isOld" label="是否年满18岁" width="120">
        </el-table-column>
        <el-table-column prop="isAgree" label="制度同意程度" width="120">
        </el-table-column>
        <el-table-column prop="isCorrect" label="资料正确性" width="120">
        </el-table-column>
        
        <el-table-column label="操作" width="200">
          
          <el-button type="text" >查看详情</el-button>
          <el-button type="text" size="large">取消申请</el-button>
          <el-dialog title="活动详情" :append-to-body="true">
          </el-dialog>
         
        </el-table-column>
      </el-table>
    </div> -->
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
      applicantInfo: {},
    };
    },

  async mounted() {
    // fetch("http://localhost:1337/student/:id/course")
    // .then(res => res.json())
    // .then(data => this.data = data)
    // .catch(err => console.log(err.message))

    var response = await fetch(
      "http://localhost:1337/student/:id/course" 
    );
    if (response.ok) {
      this.applicantInfo = await response.json();
    }
  },

  }
</script>