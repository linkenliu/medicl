<template>
    <div class="box-inner">
        <div class="box-header well" data-original-title="">
            <h2><i class="glyphicon glyphicon-user"></i>{{pageTitle || "预约挂号"}}</h2>
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
                    <label for="exampleInputEmail2">患者姓名:</label>
                    <input type="text" class="form-control" placeholder="患者姓名" value="{{query.patientName}}" v-model="query.patientName">
                </div>
                <div class="form-group">
                    <label for="exampleInputEmail2">手机号:</label>
                    <input type="text" class="form-control" placeholder="手机号" value="{{query.patientMobile}}" v-model="query.patientMobile">
                </div>
                <div class="form-group">
                    <label for="exampleInputEmail2">就诊科室:</label>
                    <select class="form-control" v-model="query.departmentId">
                        <option value="">全部</option>
                        <template v-for="depart in departments">
                        <option value="{{depart.id}}">{{depart.name}}</option>
                        </template>
                    </select>
                    <label for="exampleInputEmail2">挂号类型:</label>
                    <select class="form-control" v-model="query.registrationType">
                        <option value="">全部</option>
                        <option value="0">线上预约</option>
                        <option value="1">线下预约</option>
                        <option value="2">现场挂号</option>
                        <option value="3">复诊预约</option>
                        <option value="4">转诊挂号</option>
                        <option value="5">现场加号</option>
                        <option value="6">线上加号</option>
                        <option value="7">销售代约</option>
                        <option value="8">销售加号</option>
                    </select>
                    <label for="exampleInputEmail2">医生:</label>
                    <select class="form-control" v-model="query.doctorId">
                        <option value="">全部</option>
                        <template v-for="doctor in doctors">
                        <option value="{{doctor.id}}">{{doctor.name}}</option>
                        </template>
                    </select>
                    <label for="exampleInputEmail2">门诊状态:</label>
                    <select class="form-control" v-model="query.status">
                        <option value="">全部</option>
                        <option value="0">初诊</option>
                        <option value="1">复诊</option>
                        <option value="2">院内转诊</option>
                        <option value="3">跨院转诊</option>
                        <option value="4">远程会诊</option>
                        <option value="5">远程初诊</option>
                        <option value="6">远程复诊</option>
                    </select>
                    <label for="exampleInputEmail2">会员类型:</label>
                    <select class="form-control" v-model="query.memberType">
                        <option value="">全部</option>
                        <option value="0">初级用户</option>
                        <option value="1">银卡用户</option>
                        <option value="2">金卡用户</option>
                        <option value="3">学校用户</option>
                        <option value="4">企业用户</option>
                        <option value="5">儿童用户</option>
                    </select>
                    <button type="submit" class="btn btn-default" v-on:click="todayPatient(1, ta)">搜索</button>
                </div>
            </form>
        </div>
        <div class="box col-md-6 text-left">
            <p>
                <button class="btn btn-default btn-sm" v-on:click="showModal('mymodal1')">
                    <i class="glyphicon glyphicon-plus"></i>新增
                </button>
            </p>
        </div>
        <div class="box col-md-6 text-right">
            <p>
                <button class="btn btn-default btn-sm" v-on:click="showModal('mymodal2')">变更</button>
                <button class="btn btn-default btn-sm" v-on:click="showModal('mymodal3')">预览</button>
                <button class="btn btn-default btn-sm" v-on:click="showModal('mymodal4')">取消</button>
            </p>
        </div>
        <div class="box-content">
            <table class="table table-striped table-bordered responsive" id="groupList">
                <thead>
                    <tr>
                    	<th>选择</th>
                      <th>姓名</th>
                      <th>手机</th>
                      <th>性别</th>
                      <th>就诊时间</th>
                      <th>科室</th>
                      <th>挂号类型</th>
                      <th>医生</th>
                      <th>门诊号</th>
                      <th>门诊内容</th>
                      <th>门诊状态</th>
                      <th>挂号费</th>
                      <th>余额</th>
                      <th>会员类型</th>
                      <th>挂号时间</th>
                      <th>推荐人</th>
                      <th>预约状态</th>
                  </tr>
                </thead>
                <tbody>
                    <tr v-for="item in patients">
                    	<td class="center"><input type="radio" v-on:click="checkedItem(item.id)" value="{{item.id}}" name="registId"/></td>
                        <td class="center">{{item.patientName}}</td>
                        <td class="center">{{item.patientMobile}}</td>
                        <td class="center">{{item.gender}}</td>
                        <td class="center">{{item.registerDate | fmtDate 'MM-dd hh:mm'}}</td>
                        <td class="center">{{item.departmentName}}</td>
                        <td class="center">{{item.registrationType}}</td>
                        <td class="center">{{item.doctorName}}</td>
                        <td class="center">{{item.sequence}}</td>
                        <td class="center">{{item.comment}}</td>
                        <td class="center">{{item.status}}</td>
                        <td class="center">{{item.registrationFee}}</td>
                        <td class="center">{{item.balance}}</td>
                        <td class="center">{{item.memberType}}</td>
                        <td class="center">{{item.registerDate | fmtDate 'MM-dd hh:mm'}}</td>
                        <td class="center">{{item.businessPeopleName}}</td>
                        <td class="center">{{item.preRegistrationStatus}}</td>
                    </tr>
                </tbody>
            </table>
            <nav>
                <ul class="pager">
                    <li class=""><a @click="todayPatient(parseInt(query.pageIndex)-1, ta)">上一页</a></li>
                    <li>第{{query.pageIndex}}页</li>
                    <li ><a @click="todayPatient(parseInt(query.pageIndex)+1, ta)">下一页</a></li>
                    <li>共{{Math.ceil(query.totalCount/10)}}页</li>
                    <li>共{{query.totalCount}}条</li>
                </ul>
            </nav>
            <router-view></router-view>
        </div>
    </div>
    <!-- Modal1 -->
    <div class="modal" id="mymodal1" role="dialog" aria-labelledby="gridSystemModalLabel">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" v-on:click="showModal('mymodal1')"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="gridSystemModalLabel">创建（预约）挂号</h4>
          </div>
          <div class="modal-body">
            <form class="form-horizontal">
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">姓名</label>
                <div class="col-sm-4">
                  <input type="text" class="form-control" placeholder="姓名" v-model="registeredObj.patientName" value="{{registeredObj.patientName}}">
                </div>
                <label for="" class="col-sm-2 control-label">性别</label>
                <div class="col-sm-4">
                  <select class="form-control" v-model="registeredObj.gender">
                    <option value="">选择</option>
                    <option value="1">男</option>
                    <option value="0">女</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">手机</label>
                <div class="col-sm-4">
                  <input type="tel" class="form-control" placeholder="手机号" v-model="registeredObj.patientMobile" value="{{registeredObj.patientMobile}}">
                </div>
                <label for="" class="col-sm-2 control-label">科室</label>
                <div class="col-sm-4">
                  <select class="form-control" v-on:change="getDepartment" v-model="registeredObj.departmentId">
                    <option value="">选择</option>
                    <option v-for="depart in departments" v-bind:value="depart.id">{{depart.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">医生</label>
                <div class="col-sm-4">
                  <select class="form-control" v-model="registeredObj.doctorId" v-on:change="getRegistrationFee">
                    <option value="">选择</option>
                    <option v-for="doctor in doctors" v-bind:value="doctor.id">{{doctor.name}}</option>
                  </select>
                </div>
                <label for="" class="col-sm-2 control-label">挂号费</label>
                <div class="col-sm-4 disabled">
                    <input type="text" class="form-control" v-model="registeredObj.registrationFee" value="{{registeredObj.registrationFee}}" disabled/>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">支付方式</label>
                <div class="col-sm-4">
                  <select class="form-control" v-model="registeredObj.paymentType">
                    <option value="0">银行卡</option>
                    <option value="1">储值卡</option>
                    <option value="2">现金</option>
                    <option value="3">代付</option>
                    <option value="4">微信钱包</option>
                    <option value="5">支付宝</option>
                    <option value="6">其他</option>
                  </select>
                </div>
                <label for="" class="col-sm-2 control-label">会员类型</label>
                <div class="col-sm-4">
                  <select class="form-control" v-model="registeredObj.memberType">
                    <option value="">选择</option>
                    <option value="0">初级用户</option>
                    <option value="1">银卡用户</option>
                    <option value="2">金卡用户</option>
                    <option value="3">学校用户</option>
                    <option value="4">企业用户</option>
                    <option value="5">儿童用户</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">就诊日期</label>
                <div class="col-sm-5">
                  <input type="date" class="form-control" placeholder="日期" v-model="registeredObj.registerDate" value="{{registeredObj.registerDate}}">
                </div>
                <label for="" class="col-sm-2 control-label">就诊时段</label>
                <div class="col-sm-3">
                  <select class="form-control" v-model="registeredObj.shiftPeriod">
                    <option value="">选择</option>
                    <option v-for="period in shiftPeriods" v-bind:value="period.id">{{period.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">推荐人</label>
                <div class="col-sm-4">
                  <select class="form-control" v-model="registeredObj.businessPeopleId">
                    <option value="">选择</option>
                    <option v-for="period in busPeoples" v-bind:value="period.id">{{period.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-2 control-label">门诊内容</label>
                <div class="col-sm-10">
                  <textarea class="form-control" v-model="registeredObj.comment">{{registeredObj.comment}}</textarea>
                </div>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" v-on:click="saveRegistered">确定挂号</button>
            <button type="button" class="btn btn-default" data-dismiss="modal" v-on:click="showModal('mymodal1')">取消</button>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
    <!-- Modal2 -->
    <div class="modal" id="mymodal2" role="dialog" aria-labelledby="gridSystemModalLabel">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" v-on:click="showModal('mymodal2')"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="gridSystemModalLabel">（预约）挂号变更</h4>
          </div>
          <div class="modal-body">
            <form class="form-horizontal">
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">姓名</label>
                <div class="col-sm-5">
                  <input type="text" class="form-control" placeholder="姓名" v-model="registeredObj.patientName" value="{{registeredObj.patientName}}">
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">手机</label>
                <div class="col-sm-5">
                  <input type="tel" class="form-control" placeholder="手机号" v-model="registeredObj.patientMobile" value="{{registeredObj.patientMobile}}">
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">科室</label>
                <div class="col-sm-5">
                  <select class="form-control" v-on:change="getDepartment" v-model="registeredObj.departmentId">
                    <option value="">选择</option>
                    <option v-for="depart in departments" v-bind:value="depart.id">{{depart.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">医生</label>
                <div class="col-sm-5">
                  <select class="form-control" v-model="registeredObj.doctorId" v-on:change="getRegistrationFee">
                    <option value="">选择</option>
                    <option v-for="doctor in doctors" v-bind:value="doctor.id">{{doctor.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">日期</label>
                <div class="col-sm-5">
                  <input type="date" class="form-control" placeholder="日期" v-model="registeredObj.registerDate" value="{{registeredObj.registerDate}}">
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">时段</label>
                <div class="col-sm-5">
                  <select class="form-control" v-model="registeredObj.shiftPeriod">
                    <option value="">选择</option>
                    <option v-for="period in shiftPeriods" v-bind:value="period.id">{{period.name}}</option>
                  </select>
                </div>
              </div>
              <div class="form-group">
                <label for="" class="col-sm-3 control-label">变更原因</label>
                <div class="col-sm-9">
                  <textarea class="form-control" v-model="registeredObj.comment">{{registeredObj.comment}}</textarea>
                </div>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" v-on:click="showModal('mymodal2')">确定变更</button>
            <button type="button" class="btn btn-default" data-dismiss="modal" v-on:click="showModal('mymodal2')">取消</button>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
    <!-- Modal3 -->
    <div class="modal" id="mymodal3" role="dialog" aria-labelledby="gridSystemModalLabel">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" v-on:click="showModal('mymodal3')"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="gridSystemModalLabel">*****医院挂号单</h4>
          </div>
          <div class="modal-body">
            <p>-----------------------------------------------</p>
            <p>********科室****医生（**诊位）</p>
            <p>姓名：张三</p>
            <p>门诊日期：2015年00月00日  00:00—00:00</p>
            <p>门诊第01号</p>
            <p>-----------------------------------------------</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" v-on:click="showModal('mymodal3')">关闭</button>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
    <!-- Modal4 -->
    <div class="modal" id="mymodal4" role="dialog" aria-labelledby="gridSystemModalLabel">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" v-on:click="showModal('mymodal4')"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="gridSystemModalLabel">（预约）挂号取消</h4>
          </div>
          <div class="modal-body">
            <form class="form-horizontal">
              <div class="form-group">
                <label for="" class="col-sm-12">取消原因</label>
                <div class="col-sm-12">
                  <textarea class="form-control" rows="4"></textarea>
                </div>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" v-on:click="showModal('mymodal4')">确定</button>
            <button type="button" class="btn btn-default" data-dismiss="modal" v-on:click="showModal('mymodal4')">取消</button>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
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
                shiftPeriods:[],
                busPeoples:[],
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
                    memberType:"",
                    registrationFee:""
                },
                registeredObj:{
                	patientName:"",
                    patientMobile:"",
                    gender:"",
                    departmentId:"",
                    doctorId:"",
                    registrationFee:"",
                    businessPeopleId:"",
                    paymentType:"",
                    memberType:"",
                    moment:""
                }
            }
        },
        route:{
            data:function(transition){
                //获取url传的params参数
                this.pageTitle = transition.to.query.pageTitle;
                this.todayPatient();
                this.getDepartment();
                this.getDoctor();
            }
        },
        methods: {
            todayPatient: function(pageIdx, str){
                this.query.pageIndex = (typeof pageIdx) =="number"?pageIdx:1;
                this.query.pageSize = 10;
                var condition = this.query;
                condition["x-auth-token"] = localStorage.token;
                this.$http.get("http://121.42.171.213:8080/api/registrations/all", 
                    condition, 
                    function (data, status, request) {
                        this.patients = data.data.rows;
                        this.query.totalCount = data.data.count;
                        this.query.pageIndex = data.data.pageIndex;
                        this.isActiveA = true;
                        this.isActiveB = false;
                        this.ta="t";
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            getDepartment: function(){
                this.$http.get("http://121.42.171.213:8080/api/dict/departments", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.departments = data.data;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            getDoctor: function(){
                this.$http.get("http://121.42.171.213:8080/api/dict/doctors", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.doctors = data.data;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            getRegistrationFee: function(){
                this.$http.get("http://121.42.171.213:8080/api/doctors/"+this.registeredObj.doctorId+"/registrationFee", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.registeredObj.registrationFee = data.data.registrationFee;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            getShiftPeriods: function(){
                this.$http.get("http://121.42.171.213:8080/api/dict/shiftPeriods", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.shiftPeriods = data.data;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            getBusinessPeoples: function(){
                this.$http.get("http://121.42.171.213:8080/api/dict/businessPeoples", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.busPeoples = data.data;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            showModal: function(id){
                $("#"+id).toggle();
            	this.getShiftPeriods();
            	this.getBusinessPeoples();
            },
            saveRegistered: function(){
              //设置headers数据x-auth-token
              this.$http.headers.common['x-auth-token'] = localStorage.token;
                var condition = this.registeredObj;
                this.$http.post("http://121.42.171.213:8080/api/registrations", 
                    condition, 
                    function (data, status, request) {
                        this.showModal('mymodal1');
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+JSON.stringify(request));
                    });
            },
            checkedItem: function(id){
              //设置headers数据x-auth-token
              this.$http.headers.common['x-auth-token'] = localStorage.token;
                var condition = this.registeredObj;
                this.$http.get("http://121.42.171.213:8080/api/registrations/"+id, 
                    condition, 
                    function (data, status, request) {
                      console.log(JSON.stringify(data))
                        this.registeredObj.patientName = data.data.patientName;
                        this.registeredObj.patientMobile = data.data.patientMobile;
                        this.registeredObj.moment = data.data.moment;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+JSON.stringify(request));
                    });
            }
        }
    }
</script>