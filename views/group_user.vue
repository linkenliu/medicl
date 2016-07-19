<template>
	<div class="box-inner">
		<div class="box-header well" data-original-title="">
			<h2><i class="glyphicon glyphicon-user"></i>集团用户</h2>
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
						<option value="">全部</option>
						<option value="企业名称">企业名称</option>
						<option value="手机号">手机号</option>
					</select>
					<div class="form-group">
						<input type="text" class="form-control" placeholder="企业名称" value="" v-model="">
					</div>
					<button type="submit" class="btn btn-default" v-on:click="todayPatient(1, ta)">搜索</button>
				</div>
				<button type="button" data-toggle="modal" data-target="#myModal" class="btn btn-default col-md-offset-6" v-on:click="todayPatient(1, ta)">新增集团用户</button>
			</form>
		</div>
		<div class="box-content">
			<table class="table table-striped table-bordered responsive" id="groupList">
				<thead>
					<tr>
						<th>企业名称</th>
						<th>负责人</th>
						<th>手机号码</th>
						<th>来源</th>
						<th>推荐人</th>
						<th>折扣率</th>
						<th>返利类型</th>
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
					</tr>
				</tbody>
			</table>

		</div>
	</div>

	<!-- content ends -->
	<!--/#content.col-md-0-->

	<!-- Modal -->
	<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
		<div class="modal-dialog" role="document">
			<div class="modal-content">
				<div class="modal-header center">
					<h2 class="modal-title" id="myModalLabel">登记企业</h2>
				</div>
				<form class="form-horizontal">
					<div class="modal-body">
						<div class="box-content">
							<p class="bg-warning"></p>
							<div class="form-group">
								<label for="name" class="col-sm-3 control-label">企业名称：</label>
								<div class="col-sm-7">
									<input type="text" class="form-control" placeholder="企业名称">
								</div>
							</div>
							<div class="form-group">
								<label for="name" class="col-sm-3 control-label">负责人：</label>
								<div class="col-sm-7">
									<input type="text" class="form-control" placeholder="负责人">
								</div>
							</div>
							<div class="form-group">
								<label for="name" class="col-sm-3 control-label">手机号码：</label>
								<div class="col-sm-7">
									<input type="text" class="form-control" placeholder="手机号码">
								</div>
							</div>
							<div class="form-group">
								<label for="groupName" class="col-sm-3 control-label">来源：</label>
								<div class="col-sm-7">
									<select class="form-control" name="groupId" id="groupId">
										<option value="">陌生拜访</option>
										<option value="">市场活动</option>
										<option value="">陌生拜访</option>
									</select>
								</div>
							</div>
							<div class="form-group">
								<label for="groupName" class="col-sm-3 control-label">推荐人：</label>
								<div class="col-sm-7">
									<select class="form-control" name="groupId" id="groupId">
										<option value="">张三</option>
									</select>
								</div>
							</div>
							<div class="form-group">
								<label for="name" class="col-sm-3 control-label">折扣率：</label>
								<div class="col-sm-6">
									<input type="text" class="form-control" placeholder="折扣率">
								</div>
								<label for="name" class=" control-label">%</label>
							</div>
							<div class="form-group">
								<label for="groupName" class="col-sm-3 control-label">返现类型：</label>
								<div class="col-sm-7">
									<select class="form-control" name="groupId" id="groupId">
										<option value="">赠券</option>
										<option value="">优惠券</option>
										<option value="">免单</option>
									</select>
								</div>
							</div>
							<div class="form-group">
								<label for="" class="col-sm-3 control-label">备注:</label>
								<div class="col-sm-7">
									<textarea class="form-control" id="pushDesc" name="pushDesc" placeholder="备注"></textarea>
								</div>
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
</script>