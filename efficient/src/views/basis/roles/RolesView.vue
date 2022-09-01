<template>
	<div class="roles-box">
		<div class="header">
			角色名称:<el-input placeholder="请输入姓名" style="width: 20%"></el-input>
			<el-button icon="el-icon-search" style="margin-left: 25px" @click="search"
				>查询</el-button
			>
			<el-button icon="el-icon-refresh-right" @click="remake">重置</el-button>
			<el-button
				type="primary"
				icon="el-icon-circle-plus-outline"
				@click="addRoles"
				>新增用户</el-button
			>
		</div>
		<!-- 表格页面 -->
		<div class="table-box">
			<el-table :data="tableData" stripe style="width: 100%" border>
				<el-table-column prop="id" label="id"> </el-table-column>
				<el-table-column prop="rolename" label="角色名称"> </el-table-column>
				<el-table-column prop="remark" label="备注"> </el-table-column>
				<el-table-column label="操作">
					<template slot-scope="scope">
						<el-button size="mini" @click="handleEdit(scope.row)"
							>修改</el-button
						>
						<el-button
							size="mini"
							type="danger"
							@click="handleDelete(scope.$index, scope.row)"
							>删除</el-button
						>
					</template>
				</el-table-column>
			</el-table>
		</div>
		<!-- 分页 -->
		<div class="page-box">
			<myPagination
				:data="tableData.length"
				:currentPage="currentPage"
				:pageSize="pageSize"
				@handleSizeChange="handleSizeChange"
				@handleCurrentChange="handleCurrentChange"
			></myPagination>
		</div>

		<roles-dialog ref="roles" v-show="rolesFlag"></roles-dialog>
	</div>
</template>
<script>
import myPagination from "@/components/myPagination.vue"
import rolesDialog from "./rolesDialog.vue"
import { getRoles } from "@/utils/api"
export default {
	components: {
		myPagination,
		rolesDialog
	},
	data() {
		return {
			tableData: [],
			currentPage: 1,
			pageSize: 5,
			rolesFlag: false
		}
	},
	created() {
		/**获取角色数据 */
		getRoles().then((res) => {
			console.log(res)
			this.tableData = res.data.data
		})
	},
	mounted() {},
	methods: {
		// 分页
		handleSizeChange(val) {
			console.log(`每页 ${val} 条`)
		},
		handleCurrentChange(val) {
			console.log(`当前页: ${val}`)
		},
		/**修改 */
		handleEdit(row) {
			// console.log(row)
			this.rolesFlag = true
			this.$nextTick(() => {
				this.$refs.roles.dialogFormVisible = true
				this.$refs.roles.flag = false
				this.$refs.roles.edit(row)
			})
		},
		// 删除
		handleDelete(index, row) {
			console.log(index, row)
		},
		// 查询
		search() {},
		/**新增角色 */
		addRoles() {
			this.rolesFlag = true
			this.$nextTick(() => {
				this.$refs.roles.dialogFormVisible = true
				this.$refs.roles.flag = true
			})
		},
		// 重置
		remake() {}
	}
}
</script>

<style scoped lang="scss">
.table-box {
	width: 100%;
	margin: 20px 0;
}
::v-deep .el-input__inner {
	margin-left: 10px;
}
.header {
	width: 100%;
	display: flex;
	align-items: center;
	font-size: 18px;
}
</style>
