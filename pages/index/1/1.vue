<template>
	<view class="page-body">
		<!-- 表单开始 -->
		<vk-data-form ref="form1" v-model="form1.data" :rules="form1.props.rules" :action="form1.props.action"
			:form-type="form1.props.formType" :columns='form1.props.columns' :loading.sync="form1.props.loading"
			:label-width="100" width="100%" label-position="right" size="medium" :disabled="false" @success="formSuccess"
			@cancel="onCancel"></vk-data-form>
		<!-- 表单结束 -->
	</view>
</template>
<script>
var that; // 当前页面对象
var vk = uni.vk; // vk实例
export default {
	data() {
		return {
			// 表单相关开始-----------------------------------------------------------
			form1: {
				// 表单请求数据，此处可以设置默认值
				data: {
					"field101": [],
					"field102": [],
					"field103": 0
				},
				// 表单属性   
				props: {
					// 表单提交地址
					action: '请替换自己的路由地址',
					// 表单字段显示规则
					columns: [{
						"key": "text",
						"title": "单行文本",
						"type": "text",
						"placeholder": "请输入单行文本",
						"clearable": true,
						"showLabel": true,
						"showWordLimit": true
					}, {
						"key": "field101",
						"title": "级联选择",
						"type": "cascader",
						"placeholder": "请选择级联选择",
						"clearable": true,
						"showLabel": true,
						"action": "admin/system/permission/sys/getAll",
						"data": [{
							"id": 1,
							"value": 1,
							"label": "选项1",
							"children": [{
								"id": 2,
								"value": 2,
								"label": "选项1-1"
							}]
						}],
						"props": {
							"value": "permission_id",
							"label": "label",
							"children": "children",
							"multiple": false
						},
						"separator": "/"
					}, {
						"key": "field102",
						"title": "多选框组",
						"type": "checkbox",
						"showLabel": true,
						"data": [{
							"label": "选项一",
							"value": 1
						}, {
							"label": "选项二",
							"value": 2
						}],
						"optionType": "default",
						"size": "medium"
					}, {
						"key": "field103",
						"title": "滑块",
						"type": "slider",
						"showLabel": true,
						"min": 0,
						"max": 100,
						"step": 1
					}],
					// 表单验证规则
					rules: {
						"text": [{
							"required": true,
							"message": "单行文本不能为空",
							"trigger": "change"
						}],
						"field101": [{
							"required": true,
							"message": "级联选择不能为空",
							"trigger": "change"
						}],
						"field102": [{
							"required": true,
							"message": "多选框组不能为空",
							"trigger": "change"
						}],
						"field103": [{
							"required": true,
							"message": "滑块不能为空",
							"trigger": "change"
						}]
					},
					// 自定义表单类型，如：add 代表添加 update 代表修改，可以为空
					formType: "",
					// 是否显示表单的弹窗
					show: false,
					// 表单是否在请求中
					loading: false
				},
			}
			// 表单相关结束-----------------------------------------------------------
		}
	},
	// 监听-页面每次【加载时】执行(如:前进)
	onLoad(options = {}) {
		that = this;
		vk = that.vk;
		that.options = options;
		that.init(options);
	},
	created() {},
	mounted() {},
	methods: {
		// 页面数据初始化函数
		init(options) {},
		formSuccess() {
			console.log("表单提交了");
		},
		onCancel() {
			console.log("关闭了");
		},
	},
	// 监听器
	watch: {},
	// 过滤器
	filters: {},
	// 计算属性
	computed: {},
}

</script>
<style lang="scss" scoped>
</style>
