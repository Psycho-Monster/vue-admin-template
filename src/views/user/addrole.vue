<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="角色名称">
        <el-input v-model="form.desc" />
      </el-form-item>

      <el-table
        v-loading="listLoading"
        :data="list"
        element-loading-text="Loading"
        border
        fit
        highlight-current-row
      >
        <el-table-column align="center" label="ID" width="95">
          <template slot-scope="scope">
            {{ scope.row.id }}
          </template>
        </el-table-column>
        <el-table-column label="权限名称" width="150" align="center">
          <template slot-scope="scope">
            {{ scope.row.desc }}
          </template>
        </el-table-column>
        <el-table-column label="权限路径" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.name }}</span>
          </template>
        </el-table-column>

        <el-table-column
          align="center"
          prop="created_at"
          label="授予权限"
          width="200"
        >
          <template slot-scope="scope">
            <el-switch
              v-model="scope.row.isAuth"
              active-color="#13ce66"
              inactive-color="#ff4949"
              active-text="启用"
              inactive-text="禁用"
            >
            </el-switch>
          </template>
        </el-table-column>
      </el-table>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">添加</el-button>
        <el-button @click="onCancel">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import { rulelist, addrole } from "@/api/admin";
export default {
  data() {
    return {
      form: {
        desc: "",
      },
      list: [],
      listLoading: false,
    };
  },
  beforeMount() {
    this.listLoading = true;
    rulelist().then((response) => {
      this.list = response.rulelist;
      this.total = response.total;
      console.log(response);
      this.listLoading = false;
    });
  },
  methods: {
    onSubmit() {
      this.$message("submit!");
      this.authIds = this.list.reduce((pre, item, index) => {
        if (item.isAuth) {
          pre.push(item.id);
        }
        return pre;
      }, []);
      this.rule_ids = this.authIds.join(",");
      this.form.rule_ids = this.rule_ids;
      addrole(this.form);
      this.$router.push("/role/rolelist");
    },
    onCancel() {
      this.$message({
        message: "cancel!",
        type: "warning",
      });
    },
  },
};
</script>

<style scoped>
.line {
  text-align: center;
}
</style>

