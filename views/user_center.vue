<template>
	 <div class="box-inner">
        <div class="box-header well" data-original-title="">
            <h2><i class="glyphicon glyphicon-user"></i>员工中心</h2>
            <div class="box-icon">
                <a href="#" class="btn btn-minimize btn-round btn-default"><i
                        class="glyphicon glyphicon-chevron-up"></i></a>
                <a href="#" class="btn btn-close btn-round btn-default"><i
                        class="glyphicon glyphicon-remove"></i></a>
            </div>
        </div>
        <div class="box col-md-12">
            <form class="form-inline">
                <div class="form-group">
                    <select class="form-control" v-model="query.memberType">
                        <option value="员工姓名">员工姓名</option>
                        <option value="手机号">手机号</option>
                    </select>
                     <div class="form-group">
                    	<input type="text" class="form-control" placeholder="企业名称" value="" v-model="">
                	</div>
                </div>
                <button type="button" data-toggle="modal" data-target="#addUser" class="btn btn-default col-md-offset-7" v-on:click="todayPatient(1, ta)">新增员工</button>
           		    <div class="form-group">
                    <label for="exampleInputEmail2">部门:</label>
                    <select class="form-control" v-model="query.departmentId">
                        <option value="">全部</option>
                    </select>
                    <label for="exampleInputEmail2">岗位:</label>
                    <select class="form-control" v-model="query.registrationType">
                        <option value="">全部</option>
                        <option value="院长">院长</option>
                        <option value="科室主任">科室主任</option>
                        <option value="系统管理员">系统管理员</option>
                        <option value="主任医师">主任医师</option>
                        <option value="副主任医师">副主任医师</option>
                        <option value="主治医师">主治医师</option>
                        <option value="护士长">护士长</option>
                        <option value="挂号护士">挂号护士</option>
                        <option value="业务主管">业务主管</option>
                        <option value="业务员">业务员</option>
                        <option value="客服">客服</option>
                        <option value="人事">人事</option>
                        <option value="会计">会计</option>
                    </select>
                    <label for="exampleInputEmail2">最低折扣权:</label>
                    <select class="form-control" v-model="query.doctorId">
                        <option value="">全部</option>
                    </select>
                    <label for="exampleInputEmail2">在职状态:</label>
                    <select class="form-control" v-model="query.status">
                        <option value="">全部</option>
                        <option value="试用">试用</option>
                        <option value="在职">在职</option>
                        <option value="禁用">禁用</option>
                        <option value="离职">离职</option>
                    </select>
                    <button type="submit" class="btn btn-default" v-on:click="todayPatient(1, ta)">搜索</button>
                </div>
            </form>
        </div>
        <div class="box-content">
            <table class="table table-striped table-bordered responsive" id="groupList">
                <thead>
                    <tr>
                        <th>编号</th>
                        <th>姓名</th>
                        <th>手机</th>
                        <th>性别</th>
                        <th>年龄</th>
                        <th>部门</th>
                        <th>岗位</th>
                        <th>最低折扣权</th>
                        <th>在职状态</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center"></td>
                        <td class="center">
                        	<a data-toggle="modal" data-target=".updatePassword" class="btn btn-default">修改密码</a>
                        	<br />
                        	<a class="btn btn-default">删除员工</a>
                        </td>
                    </tr>
                </tbody>
            </table>
            
        </div>
    </div>

    <!-- content ends -->
    
    
 <!--
 	作者：linken
 	时间：2015-12-17
 	描述：新建员工信息
 -->
<div class="modal fade" id="addUser" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
	<div class="modal-dialog" role="document">
		<div class="modal-content">
			<div class="modal-header center">
				<h2 class="modal-title" id="myModalLabel">新建员工信息</h2>
			</div>
			<form class="form-horizontal">
				<div class="modal-body">
					<div class="box-content">
						<div class="col-sm-8">
						<div class="form-group">
							<label for="name" class="col-sm-4 control-label">名称：</label>
							<div class="col-sm-8">
								<input type="text" class="form-control" placeholder="名称">
							</div>
						</div>
						<div class="form-group">
							<label for="groupName" class="col-sm-4 control-label">性别：</label>
							<div class="col-sm-8">
								<select class="form-control" name="groupId" id="groupId">
									<option value="男">男</option>
									<option value="女">女</option>
								</select>
							</div>
						</div>
						<div class="form-group">
							<label for="name" class="col-sm-4 control-label">手机号码：</label>
							<div class="col-sm-8">
								<input type="text" class="form-control" placeholder="手机号码">
							</div>
						</div>
						<div class="form-group">
							<label for="groupName" class="col-sm-4 control-label">部门：</label>
							<div class="col-sm-8">
								<select class="form-control" name="groupId" id="groupId">
									<option value="">选择</option>
								</select>
							</div>
						</div>
						<div class="form-group">
							<label for="groupName" class="col-sm-4 control-label">岗位：</label>
							<div class="col-sm-8">
								<select class="form-control" name="groupId" id="groupId">
									<option value="">选择</option>
								</select>
							</div>
						</div>
						<div class="form-group">
							<label for="groupName" class="col-sm-4 control-label">在职状态：</label>
							<div class="col-sm-8">
								<select class="form-control" name="groupId" id="groupId">
									<option value="">选择</option>
									<option value="">试用</option>
									<option value="">在职</option>
									<option value="">禁用</option>
									<option value="">离职</option>
								</select>
							</div>
						</div>
						<div class="form-group">
							<label for="name" class="col-sm-4 control-label">折扣率：</label>
							<div class="col-sm-7">
								<input type="text" class="form-control" placeholder="折扣率">
							</div>
							<label for="name" class=" control-label">%</label>
						</div>
						</div>
						<div class="col-sm-4">
							<div class="col-sm-12" style="border: 1px solid gray;height: 180px;">
							</div>
							<a class="btn btn-default col-sm-6 col-sm-offset-3"> 上传照片 </a>
						</div>
						<div class="form-group">
						</div>
					</div>
				</div>
			</form>
			<div class="modal-footer center">
				<button type="button" class="btn btn-default">保存</button>
				<button type="button" class="btn btn-default" data-dismiss="modal">取消</button>
			</div>
		</div>
	</div>
</div>
 <!--
 	作者：linken
 	时间：2015-12-17
 	描述：修改员工密码
 -->
 <div class="modal fade updatePassword" tabindex="-1" role="dialog" aria-labelledby="mySmallModalLabel">
	<div class="modal-dialog modal-sm">
		<div class="modal-content">
			<div class="modal-header center">
				<h2 class="modal-title" id="myModalLabel">修改员工密码</h2>
			</div>
			<form class="form-horizontal">
				<div class="modal-body">
					<div class="box-content">
						<div class="form-group">
							<label for="name" class="col-sm-5 control-label">员工姓名:</label>
							<div class="col-sm-7">
								<label for="name" class=" control-label">张三</label>
							</div>
						</div>
						<div class="form-group">
							<label for="name" class="col-sm-5 control-label">修改密码:</label>
							<div class="col-sm-7">
								<input type="text" class="form-control" placeholder="修改密码">
							</div>
						</div>
						<div class="form-group">
							<label for="name" class="col-sm-5 control-label">确认密码:</label>
							<div class="col-sm-7">
								<input type="text" class="form-control" placeholder="确认密码">
							</div>
						</div>
					</div>
				</div>
			</form>
			<div class="modal-footer center">
				<button type="button" class="btn btn-default">保存</button>
				&nbsp;&nbsp;&nbsp;&nbsp;
				<button type="button" class="btn btn-default" data-dismiss="modal">取消</button>
			</div>
		</div>
	</div>
</div>
</template>
<script>
	module.exports= {
	        replace:true,
	        props: ['pageTitle'],
	        data: function(){
	            return {
	                patients: [],
	                show: false,
	                departments: [],
	                doctors: [],
	                isActiveA:true,
	                isActiveB:false,
	                ta: "t",
	                query:{
	                    totalCount: 0,
	                    pageIndex: 0,
	                    patientName:"",
	                    patientMobile:"",
	                    departmentId:"",
	                    registrationType:"",
	                    doctorId:"",
	                    status:"",
	                    memberType:""
	                }
	            }
	        },
	        route:{
	            data:function(transition){
	                //获取url传的params参数
	                this.pageTitle = transition.to.query.pageTitle;
	            }
	        },
	        methods: {
	            allPatient: function(){
	                alert("全部患者");
	            }
	        }
	    }
	$("tbody tr").dblclick(function(){
		$('#addUser').modal('show');
	});
</script>