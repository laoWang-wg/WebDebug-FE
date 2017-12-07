<template>
    <div class="index-box">
       <top></top>
       <div class="main">
           <el-tabs v-model="activeName" @tab-click="handleClick">
               <el-tab-pane label="tab1" name="first">
                   <el-input v-model="searchContent"
                    prefix-icon="el-icon-search"></el-input>
                   <el-button type="primary" @click="search">Query</el-button>
                   <div class="card-content clear">
                       <div class="list1 list">
                           <span>list-1</span>
                           <ul>
                               <li v-for="(item,index) in list1" :key="item" @click.prevent="choseList1(index)"
                                 :class="index == currentIndex1 ? 'li-active' : ''">{{"列表"+item}}</li>
                           </ul>
                       </div>
                       <div class="list2 list">
                           <span>list-2</span>
                           <ul>
                               <li v-for="(item,ltIndex) in list2" :key="item+ltIndex" @click.prevent="choseList2(ltIndex)" 
                               :class="ltIndex == currentIndex2 ? 'li-active' : ''">{{"列表"+item}}</li>
                           </ul>
                       </div>
                       <div class="table-list">
                           <el-table :data="tableData" style="width: 100%" border stripe size="mini">
                               <el-table-column v-for="(v,k,tIndex) in tableData[0]" :key="v" :label="k" :prop="k"></el-table-column>
                               <el-table-column label="操作" fixed="right" width="100">
                                    <template slot-scope="scope">
                                        <el-button @click.native="edit(scope.row)" type="text" size="small">编辑</el-button>
                                        <el-button @click.native="del(scope.$index, scope)" type="text" size="small">删除</el-button>
                                   </template>
                               </el-table-column>
                           </el-table>
                       </div>
                   </div>
               </el-tab-pane>
               <el-tab-pane label="tab2" name="second">tab2</el-tab-pane>
               <el-tab-pane label="tab3" name="third">tab3</el-tab-pane>

               <el-dialog title="编辑" :visible.sync="dialogVisible">
                   <div class="dialog-con clearfix" v-for="(v,k,index) of dialogContent">
                      <div>{{k}}:</div>
                      <div contenteditable class="div-input" @focus="getVal(k,index)" @blur="changeValue(k,index)">{{v}}</div>
                   </div>
                   <div class="btn-box">
                       <el-button @click="editConfirm()" size="mini" type="primary">确定</el-button>
                       <el-button @click="dialogVisible = false" size="mini">取消</el-button>
                   </div>
               </el-dialog>
           </el-tabs>
       </div>
    </div>
</template>

<script>
    import Top from './top'
    export default {
        components: {
            Top,

        },
        data(){
            return {
                activeName: 'first',
                searchContent: '',
                currentIndex1: 0,
                currentIndex2: 0,
                list1:[1,2,3,4],
                list2: [5,6,7,8,9,10],
                // tableDataCol: {},
                // tableData: [],
                tableDataCol: {id: 'id', name: 'name', page: 'page', delay: 'delay'},

                tableData: [{
                    id: 1,
                    name: 'qqq',
                    page: 'asdfsdf',
                    delay: 0,
                }, {
                    id: 2,
                    name: 'www',
                    page: 'sdfsfsdafsadfsdfasd',
                    delay: 0
                }, {
                    id: 3,
                    name: 'egfdsgfdsee',
                    page: 'gdfgdf',
                    delay: 0
                }],
                tempVal: '',
                dialogContent: {},
                dialogVisible: false,
            }
        },
        methods: {
            handleClick(tab, event){
                console.log(tab, event)
            },
            search(){
                alert(this.searchContent)
            },
            choseList1(index){
                this.currentIndex1 = index
            },
            choseList2(index){
                this.currentIndex2 = index
            },
            edit(row){
                this.dialogContent = row
                this.dialogVisible = true
            },
            del(index, scope){
                this.tableData.splice(index, 1)
            },
            getVal(k,index){
                var nodeObj = document.querySelectorAll(".div-input")[index]
                this.tempVal = nodeObj.innerHTML
            },
            changeValue(k,index){
                var nodeObj = document.querySelectorAll(".div-input")[index]
                var val = nodeObj.innerHTML
                if(this.tempVal != val){
                    this.dialogContent[k] = val
                    console.log(this.dialogContent[k])
                }
            },
            editConfirm(){
                console.log(this.dialogContent)
                this.dialogVisible = false
            },

        },
    }
</script>

<style lang="scss">
    .index-box{
        background: #f0f0f0;
        padding-bottom: 20px;
        .main{
            min-height: 800px;
            margin: 20px 50px;
            padding: 5px 20px;
            border: 1px solid #DFE4ED;
            border-radius: 5px;
            background-color: #fff;
            .el-tab-pane{
                .el-input{
                    width: 90%;
                }
            }
            .card-content{
                overflow: hidden;
                .list{
                    width: 10%;
                    float: left;
                    margin:15px 20px;
                    font-size: 14px;
                    &>span{
                        display: block;
                        background-color: #d9edf6;
                        height: 36px;
                        line-height: 36px;
                        color: #466f85;
                        text-align: center;
                        margin-bottom: 8px;
                        border-radius: 4px;
                    }
                    &>ul{
                        border: 1px solid #e5e5e5;
                        border-radius: 4px;
                        &>li{
                            border-top: 1px solid #e5e5e5;
                            line-height: 25px;
                            padding: 5px 10px;
                            word-break: break-word;
                            cursor: pointer;
                        }
                        &>li:first-child{
                            border-top: none;
                        }
                        .li-active{
                            background-color: #def0d8;
                            color: #4d7f4e;
                        }
                    }
                }
                .table-list{
                    float: left;
                    width: 70%;
                    padding-top: 15px;
                }
                .text{
                    font-size: 14px;
                }
                .item{
                    margin-bottom: 18px;
                }
            }
            .dialog-con{
                padding: 4px 24px;
                &>div{
                    float: left;
                }
                .div-input{
                    min-width: 150px;
                    border: 1px solid #eee;
                    padding: 2px 4px;
                    border-radius: 4px;
                }
                &>div:first-child{
                    width: 50px;
                    margin-right: 10px;
                }
            }
            .btn-box{
                padding-top: 15px;
                padding-left: 100px;
            }
        }
    }
</style>