<template>
    <div class="box-inner">
        <div class="box-header well" data-original-title="">
            <h2><i class="glyphicon glyphicon-user"></i>{{pageTitle || "今日工作"}}</h2>
            <div class="box-icon">
                <a href="#" class="btn btn-minimize btn-round btn-default"><i
                        class="glyphicon glyphicon-chevron-up"></i></a>
                <a href="#" class="btn btn-close btn-round btn-default"><i
                        class="glyphicon glyphicon-remove"></i></a>
            </div>
        </div>
        <ul class="nav nav-tabs">
            <li role="presentation" v-bind:class="{'active': isActiveA}"><a v-on:click="todayPatient(1)">今日患者</a></li>
            <li role="presentation" v-bind:class="{'active': isActiveB}"><a v-on:click="allPatient(1)">全部患者</a></li>
        </ul>
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
        <div class="box-content">
            <table class="table table-striped table-bordered responsive" id="groupList">
                <thead>
                    <tr>
                        <th>序号</th>
                        <th>患者名称</th>
                        <th>手机号</th>
                        <th>性别</th>
                        <th>就诊时间</th>
                        <th>就诊科室</th>
                        <th>挂号类型</th>
                        <th>医生</th>
                        <th>门诊内容</th>
                        <th>门诊状态</th>
                        <th>门诊金额</th>
                        <th>卡内余额</th>
                        <th>会员类型</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in patients">
                        <td class="center">{{$index+1}}</td>
                        <td class="center">{{item.patientName}}</td>
                        <td class="center">{{item.patientMobile}}</td>
                        <td class="center">{{item.gender}}</td>
                        <td class="center">{{item.registerDate | fmtDate 'MM-dd hh:mm'}}</td>
                        <td class="center">{{item.departmentName}}</td>
                        <td class="center">{{item.registrationType}}</td>
                        <td class="center">{{item.doctorName}}</td>
                        <td class="center">{{item.comment}}</td>
                        <td class="center">{{item.status}}</td>
                        <td class="center">{{item.registrationFee}}</td>
                        <td class="center">{{item.balance}}</td>
                        <td class="center">{{item.memberType}}</td>
                        <td class="center" v-show="show">{{item.memberCardNo}}</td>
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
                this.todayPatient();
                this.getDepartment();
                this.getDoctor();
            }
        },
        methods: {
            allPatient: function(pageIdx){
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
                        this.isActiveA = false;
                        this.isActiveB = true;
                        this.ta="a"
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            },
            todayPatient: function(pageIdx, str){
                if(str == "a"){
                    this.allPatient(pageIdx);
                    return;
                }
                this.query.pageIndex = (typeof pageIdx) =="number"?pageIdx:1;
                this.query.pageSize = 10;
                var condition = this.query;
                condition["x-auth-token"] = localStorage.token;
                this.$http.get("http://121.42.171.213:8080/api/registrations/today", 
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
                //121.42.171.213
                this.$http.get("http://121.42.171.213:8080/api/dict/doctors", 
                    {"x-auth-token":localStorage.token}, 
                    function (data, status, request) {
                        this.doctors = data.data;
                    }).error(function (data, status, request) {
                        console.log("err:"+data+"status:"+status+"request:"+request);
                    });
            }
        }
    }
</script>