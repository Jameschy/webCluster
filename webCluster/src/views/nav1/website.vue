<template>
	<section>
		<!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true" :model="filters">
				<el-form-item>
					<el-input v-model="filters.webname" placeholder="网站名称"></el-input>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" v-on:click="getWebsite">查询</el-button>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="getWebsite">新增</el-button>
				</el-form-item>
			</el-form>
		</el-col>

		<!--列表Website-->
		<template>
			<el-table :data="Website" highlight-current-row v-loading="loading" style="width: 100%;">
				<el-table-column type="index" width="60">
				</el-table-column>
				<el-table-column prop="web_name" label="网站名称" width="120" sortable>
				</el-table-column>
				<el-table-column prop="web_status" label="状态" width="100" :formatter="formatStatus" sortable>
				</el-table-column>
				<el-table-column prop="web_click" label="点击量" width="100" sortable>
				</el-table-column>
				<el-table-column prop="web_addtimes" label="添加日期" width="120" sortable>
				</el-table-column>
				<el-table-column prop="web_addr" label="网站地址" min-width="180" sortable>
				</el-table-column>
			</el-table>
		</template>

	</section>
</template>
<script>
    import { getWebsiteList } from '../../api/api';
    //import NProgress from 'nprogress'
    export default {
        data() {
            return {
                filters: {
                    web_name: ''
                },
                loading: false,
                Website: [
                ]
            }
        },
        methods: {
            //性别显示转换
            formatStatus: function (row, column) {
                return row.web_status == 1 ? '启用' : row.web_status == 0 ? '禁用' : '未知';
            },
            //获取用户列表
            getWebsite: function () {
                let para = {
                    web_name: this.filters.web_name
                };
                this.loading = true;
                //NProgress.start();
                getWebsiteList(para).then((res) => {
                    this.website = res.data.website;
                    this.loading = false;
                    //NProgress.done();
                });
            }
        },
        mounted() {
            this.getWebsite();
        }
    };

</script>

<style scoped>

</style>
