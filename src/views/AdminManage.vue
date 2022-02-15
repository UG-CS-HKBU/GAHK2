<template>
<div>
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
    </div>


<!-- <div> -->
  <!-- <el-table :data="list3" border style="width: 100%">
        <el-table-column type="expand">
          <template slot-scope="props">
            <el-form label-position="left" inline class="demo-table-expand">
              <el-form-item label="课程编码">
                <span>{{ props.row.code }}</span>
              </el-form-item><br>
              <el-form-item label="姓名">
                <span>{{ props.row.address }}</span>
              </el-form-item><br>
            </el-form>
          </template>
        </el-table-column>

        <template>
          <el-table-column type="index" label="id" width="120"> </el-table-column>
          <el-table-column prop="address" label="活动名称" width="120"> </el-table-column>

          <el-table-column label="操作" width="200">
             <router-link to="/applicationform">去申请页面</router-link>
          </el-table-column>
        </template>
      </el-table>
  </div> -->
</template>

<script>
  export default {
    data() {
      return {
        list3: []
      }
    },

     mounted() {
    fetch('http://localhost:1337/student/:id/course')
    .then(res => res.json())
    .then(data => this.list3 = data)
    .catch(err => console.log(err.message))
  },

  }
</script>