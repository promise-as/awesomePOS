<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id='order-list'>
        <el-tabs stretch>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border>
              <el-table-column prop="goodsName" label="商品名称" align="center"></el-table-column>
              <el-table-column prop="count" label="数量" align="center"></el-table-column>
              <el-table-column prop="price" label="金额" align="center"></el-table-column>
              <el-table-column label="操作" align="center" fixed="right">
                <template slot-scope="scope">
                  <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="totalDiv">
              <small>数量：</small>{{totalCount}} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <small>金额：</small>{{totalMoney}}元
            </div>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods">删除</el-button>
              <el-button type="success" @click="cleckout">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">
            挂单

          </el-tab-pane>
          <el-tab-pane label="外卖">
            外卖

          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span='17'>
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="(goods,index) in oftenGoods" :key="index" @click="addOrderList(goods)">
                <span >{{goods.goodsName}}</span>
                <span class="o-price">￥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs stretch>
            <el-tab-pane label="汉堡">
              <div>
                <ul class="cookList">
                  <li v-for="(goods, index) in type0Goods" :key='index' @click="addOrderList(goods)">
                   <span class="foodImg"><img :src="goods.goodsImg"/></span>
                   <span class="foodName">{{goods.goodsName}}</span>
                   <span class="foodPrice">{{goods.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食">
              小食
            </el-tab-pane>
            <el-tab-pane label="饮料">
              饮料
            </el-tab-pane>
            <el-tab-pane label="套餐">
              套餐
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>

export default {
  name: 'pos',
  data(){
    return{
      /* tableData: [
        {
          goodsName: '可口可乐',
          price: 8,
          count: 1,
        },
        {
          goodsName: '香辣鸡腿堡',
          price: 15,
          count: 1
        },
        {
          goodsName: '爱心薯条',
          price: 8,
          count: 1
        },
        {
          goodsName: '甜筒',
          price: 8,
          count: 1
        }
      ], */
      tableData: [],
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: '香辣鸡腿堡',
          price:18
        },
        {
          goodsId: 2,
          goodsName: '田园鸡腿堡',
          price:15
        },
        {
          goodsId: 3,
          goodsName: '和风汉堡',
          price:15
        },
        {
          goodsId: 4,
          goodsName: '快乐全家桶',
          price:80
        },
        {
          goodsId: 5,
          goodsName: '脆皮炸鸡腿',
          price:10
        },
        {
          goodsId: 6,
          goodsName: '魔法鸡块',
          price:20
        },
        {
          goodsId: 7,
          goodsName: '可乐大杯',
          price:10
        },
        {
          goodsId: 8,
          goodsName: '雪顶咖啡',
          price:18
        },
        {
          goodsId: 9,
          goodsName: '大块鸡米花',
          price:15
        },
        {
          goodsId: 10,
          goodsName: '香脆鸡柳',
          price:17
        }
      ],
      type0Goods: [
        {
          goodId: 1,
          goodsImg: "https://ae01.alicdn.com/kf/Headdf5420e9446d8aa8c376c052c3cccv.jpg",
          goodsName: "香辣鸡腿堡",
          price: 18
        },
        {
          goodId: 2,
          goodsImg: "https://ae01.alicdn.com/kf/H31ee6985d7d94aef8c7a6bfd1ce9fe04s.jpg",
          goodsName: "新奥尔良烤鸡腿堡",
          price: 15
        },
        {
          goodId: 3,
          goodsImg: "https://ae01.alicdn.com/kf/Hbc4068f5f1b44a6992adb6c8c7b2c91f7.jpg",
          goodsName: "超级外送全家桶",
          price: 128
        },
        {
          goodId: 4,
          goodsImg: "https://ae01.alicdn.com/kf/H06a9fcc357d84f3b9af0eabc5fc10f87d.jpg",
          goodsName: "二块新奥尔良烤翅",
          price: 12.5
        },
        {
          goodId: 5,
          goodsImg: "https://ae01.alicdn.com/kf/H053004ae3de14fbf84736d90a343d09fH.jpg",
          goodsName: "黄金鸡块5块装",
          price: 11.5
        },
        {
          goodId: 6,
          goodsImg: "https://ae01.alicdn.com/kf/H2badc469f02a45b9953f79e26b3ffa18F.jpg",
          goodsName: "百事可乐(中)",
          price: 9.5
        },
      ],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      type4Goods: [],
      totalMoney: 0,
      totalCount: 0
    }
  },
  mounted: function(){
    var orderHeihgt = document.body.clientHeight;
    document.getElementById('order-list').style.height = orderHeihgt + 'px';
  },
  methods: {
    addOrderList(goods){

      this.totalMoney = 0;
      this.totalCount = 0;
      
      // 商品是否已经存在于订单列表中
      let isHave = false;
      for(let i = 0; i < this.tableData.length; i++){
        if(this.tableData[i].goodsId == goods.goodsId){
          isHave = true;
        }
      }

      // 根据判断的值编写业务逻辑
      if(isHave){
        // 改变列表中商品数量
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
        arr[0].count++;
      }else{
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        }
        this.tableData.push(newGoods);
      }
      this.getAllMoney();
      
    },
    // 删除单个商品
    delSingleGoods(goods){
      this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId)
      this.getAllMoney();
    },
    delAllGoods(){
      this.tableData = [],
      this.totalCount = 0;
      this.totalMoney = 0
    },
    // 模拟结账
    cleckout(){
      if(this.totalCount != 0){
        this.tableData = [],
        this.totalCount = 0;
        this.totalMoney = 0
        this.$message({
          message: '结账成功，感谢你又为店里出了一份力',
          type: 'success'
        })
      }else{
        this.$message.error('不能空结，老板了解你急切的心情！')
      }
    },
    // 汇总数量金额
    getAllMoney(){
      this.totalCount = 0;
      this.totalMoney = 0;
      // 计算汇总金额和数量
      if(this.tableData){
        this.tableData.forEach((element) => {
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + (element.price * element.count);
        })
      }
     
    }
  }
}
</script>

<style scoped>
  .pos-order{
    background-color: #F9FAFC;
    border-right: 1px solid #C0CCDA;
  }
  .div-btn{
    margin-top: 10px;
  }
  .title{
    height: 20px;
    border-bottom: 1px solid #d3dce6;
    background-color: #F9FAFC;
    padding: 10px;
    text-align: left;
  }
  .often-goods-list ul li{
    list-style: none;
    float: left;
    border: 1px solid #E5E9F2;
    padding: 10px;
    margin: 10px;
    background-color: #fff;
    cursor: pointer;
  }
  .o-price{
    color: #58B7FF;
  }
  .goods-type{
    clear: both;
  }
  .cookList li{
    list-style: none;
    width: 23%;
    border: 1px solid #E5E9F2;
    height: auto;
    overflow: hidden;
    background-color: #fff;
    padding: 2px;
    float: left;
    margin: 10px;
    cursor: pointer;
  }
  .cookList li span{
    display: block;
    float: left;
  }
  .foodImg{
    width: 40%;
  }
  .foodImg img{
    width: 100%;
  }
  .foodName{
    width: 55%;
    font-size: 18px;
    padding-left: 10px;
    color: brown;
    text-align: left;
  }
  .foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top: 10px;
  }
  .totalDiv{
    background-color: #fff;
    padding: 10px;
    border-bottom: 1px solid #EBEEF5;
  }
</style>
