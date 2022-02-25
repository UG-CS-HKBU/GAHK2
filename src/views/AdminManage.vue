<template>
  <div>
    <h2>{{ applicantInfo }}</h2>
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

      <o-table-column label="操作">
          <button>同意</button>
           <button>拒绝</button> 
      </o-table-column>
    </o-table>

    <!-- <div>
      <el-table :data="list3" border style="width: 100%">
        <el-table-column type="index" label="id" width="80">
        </el-table-column>
        <el-table-column prop="item" label="活動項目" width="120">
        </el-table-column>
        <el-table-column prop="code" label="活動編碼" width="120">
        </el-table-column>
         <el-table-column prop="level" label="難度" width="120">
        </el-table-column>
         <el-table-column prop="Ename" label="緊急聯繫人姓名" width="120">
        </el-table-column>
        <el-table-column prop="tel" label="緊急聯繫人電話" width="120">
        </el-table-column>
        <el-table-column prop="address" label="住址" width="120">
        </el-table-column>
        <el-table-column prop="paying" label="付款方式" width="120">
        </el-table-column>
        <el-table-column prop="isOld" label="是否年滿18歲" width="120">
        </el-table-column>
        <el-table-column prop="isAgree" label="制度同意程度" width="120">
        </el-table-column>
        <el-table-column prop="isCorrect" label="資料正確性" width="120">
        </el-table-column>
        
        <el-table-column label="操作" width="200">
          
          <el-button type="text" >查看詳情</el-button>
          <el-button type="text" size="large">取消申請</el-button>
          <el-dialog title="活動詳情" :append-to-body="true">
          </el-dialog>
         
        </el-table-column>
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
      applicantInfo: {},
    };
  },

  async mounted() {
    // fetch("http://localhost:1337/student/:id/course")
    // .then(res => res.json())
    // .then(data => this.data = data)
    // .catch(err => console.log(err.message))

    var response = await fetch("http://localhost:1337/student/:id/course");
    if (response.ok) {
      this.applicantInfo = await response.json();
    }
  },
};
</script>