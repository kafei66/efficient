<template>
	<div>
		<el-dialog
			:title="flag ? '新增角色' : '修改角色'"
			:visible.sync="dialogFormVisible"
			:before-close="close"
		>
			<el-form
				:model="ruleForm"
				:rules="rules"
				ref="ruleForm"
				label-width="100px"
				class="demo-ruleForm"
			>
				<el-form-item label="活动名称" prop="rolename">
					<el-input v-model="ruleForm.rolename" style="width: 200px"></el-input>
				</el-form-item>
				<el-form-item label="活动名称" prop="options">
					<el-cascader
						:options="ruleForm.options"
						:props="props"
						clearable
						style="width: 200px"
					></el-cascader>
				</el-form-item>
				<el-form-item label="活动名称" prop="remark">
					<el-input
						type="textarea"
						:rows="2"
						placeholder="请输入内容"
						v-model="ruleForm.remark"
						style="width: 200px"
					>
					</el-input>
				</el-form-item>

				<el-form-item>
					<el-button type="primary" @click="submitForm('ruleForm')"
						>立即创建</el-button
					>
					<el-button @click="resetForm('ruleForm')">重置</el-button>
				</el-form-item>
			</el-form>
		</el-dialog>
	</div>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			dialogFormVisible: false,
			flag: true,
			props: { multiple: true },
			ruleForm: {
				rolename: "",
				remark: "",
				options: [
					{
						value: 1,
						label: "亚洲",
						children: [
							{
								value: 2,
								label: "中国",
								children: [{ value: 3, label: "上海" }]
							}
						]
					},
					{
						value: 17,
						label: "北美洲",
						children: [
							{
								value: 18,
								label: "美国"
							}
						]
					}
				]
			},
			rules: {
				rolename: [
					{ required: true, message: "请输入角色名称", trigger: "blur" },
					{ min: 1, max: 6, message: "长度在 1 到 6 个字符", trigger: "blur" }
				],
				options: [
					{ required: true, message: "请选择活动区域", trigger: "change" }
				],
				remark: [{ required: true, message: "请输入备注", trigger: "blur" }]
			}
		}
	},
	created() {},
	mounted() {},
	methods: {
		edit(row) {
			this.form = row
		},
		/**关闭的回调 */
		close() {
			this.dialogFormVisible = false
			// console.log(this.$refs.ruleForm)
			this.$refs.ruleForm.resetFields()
		}
	}
}
</script>

<style scoped lang="scss"></style>
