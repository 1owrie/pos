<template>
  <div class="pos">
    <div>
      <el-row>
        <el-col :span="6" class="pos-order" id="order-list">
          <div class="tabs-div">
            <el-tabs>
              <el-tab-pane label="点餐">
                <el-table border show-summary style="width: 100%" :data="tableData">
                  <el-table-column prop="goodsName" label="商品" align="center" header-align="center"></el-table-column>
                  <el-table-column prop="count" label="数量" width="70" align="center"></el-table-column>
                  <el-table-column prop="price" label="金额" width="70" align="center"></el-table-column>
                  <el-table-column label="操作" width="100" fixed="right">
                    <template slot-scope="scope">
                      <el-button type="text" size="small" @click="addBtn(scope.row)">增加</el-button>
                      <el-button type="text" size="small" @click="deleteBtn(scope.$index,scope.row)">删除</el-button>
                    </template>
                  </el-table-column>
                </el-table>
              </el-tab-pane>
              <el-tab-pane label="挂单">
                挂 单
              </el-tab-pane>
              <el-tab-pane label="外卖">
                外 卖
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-col>

        <!--商品展示-->
        <el-col :span="18" id="order-more">
          <div class="hot-food">热门商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="item in hotFood" @click="addHot(item)">
                <span>{{ item.goodsName }}</span>
                <span class="o-price">￥{{item.price}}元</span>
              </li>
            </ul>
            <div class="tabs-div">
              <el-tabs v-model="activeName">
                <el-tab-pane label="汉堡" name="first">
                  <ul class="more-ul">
                    <li v-for="food in moreFood">
                      <span class="foodImg"><img src="../../assets/1.jpg" width="100%" height="100%"></span>
                      <span class="foodName">{{food.goodsName}}</span>
                      <span class="foodPrice">￥{{food.price}}元</span>
                    </li>
                  </ul>
                </el-tab-pane>
                <el-tab-pane label="小食" name="second">小食</el-tab-pane>
                <el-tab-pane label="饮料" name="third">饮料</el-tab-pane>
                <el-tab-pane label="套餐" name="fourth">套餐</el-tab-pane>
              </el-tabs>
            </div>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Pos",
  data() {
    return {
      hotFood: [],
      moreFood: [],
      activeName: "first",
      tableData: []
    };
  },
  mounted: function() {
    var h = document.body.clientHeight;
    document.getElementById("order-list").style.height = h + "px";
    document.getElementById("order-more").style.height = h + "px";
  },
  created: function() {
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
      )
      .then(response => {
        this.hotFood = response.data;
        this.moreFood = response.data;
        console.log(response);
      })
      .catch(error => {
        alert("网络错误");
      });
  },
  methods: {
    addHot(item) {
      let isHave = false;
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsName == item.goodsName) {
          isHave = true;
        }
      }
      if (isHave) {
        let arr = this.tableData.filter(i => i.goodsName == item.goodsName);
        arr[0].count++;
        arr[0].price=arr[0].price+item.price;
      } else {
        let o = {
          goodsName: item.goodsName,
          price: item.price,
          count: 1
        };       
        this.tableData.push(o);
        console.log(this.tableData);
        
      }

    },
    addBtn(row) {
      row.price = row.price + row.price / row.count;
      row.count++;
    },
    deleteBtn(index, row) {
      row.price = row.price - row.price / row.count;
      row.count--;
      if (row.count == 0) {
        this.tableData.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
.pos {
  width: 95%;
  float: left;
}

.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}

.tabs-div {
  padding: 10px;
}

.hot-food {
  width: 100%;
  text-align: left;
  padding: 14px;
  border-bottom: 1px solid #d3dce6;
  height: 20px;
}

.often-goods-list {
  text-align: left;
}

.often-goods-list li {
  list-style: none;
  display: inline-block;
  margin: 10px 10px;
  border: 1px solid #e5e9f2;
  cursor: pointer;
}

.o-price {
  color: #58b7ff;
}

.foodImg {
  width: 40%;
  height: 100%;
}

.more-ul li {
  list-style: none;
  padding: 0px;
  width: 260px;
  height: 120px;
  cursor: pointer;
}

.more-ul li span {
  display: block;
  float: left;
}

.foodName {
  margin: 5% 0 5% 5%;
  color: red;
  font-size: 18px;
  width: 55%;
}

.foodPrice {
  font-size: 16px;
  margin: 0 0 0 5%;
  width: 55%;
}
</style>
