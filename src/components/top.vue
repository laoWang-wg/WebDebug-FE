<template>
	<div class="top-con clear">
		<a href="#" class="left home">Home</a>
		<div class="right right-con">
			<a href="#">GitHub</a>
			<el-dropdown trigger="click">
			  <span class="el-dropdown-link">
			    other<i class="el-icon-arrow-down el-icon--right"></i>
			  </span>
			  <el-dropdown-menu slot="dropdown">
			    <el-dropdown-item><a href="http://www.baidu.com">aaa</a></el-dropdown-item>
			    <el-dropdown-item><a href="#">bbb</a></el-dropdown-item>
			  </el-dropdown-menu>
			</el-dropdown>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		}
	}
</script>

<style lang="scss">
.top-con{
	width: 100%;
	height: 50px;
	line-height: 50px;
	background-color: #409EFF; 
	& a{
		color: #fff;
	}
	.home{
		margin-left: 50px;
	}
	.right-con{
		margin-right: 50px;
		&>a{
			margin-right: 20px;
		}
	}		    
	.el-dropdown-link{
		color: #fff;
	}
}
	
</style>