<script setup lang="ts">
import { ref } from "vue";
// import data from '../../../data.json'
// defineProps<{ msg: string}>();
const borderColor2 = ref("1px solid #4EA6FF");
const borderColor1 = ref("1px solid #dcdcdc");
const cardShow = ref("block");
const tableShow = ref("none");
const show = ref(2);
const data = ref([
  {
    productCategory: "家教机",
    prjCategory: "教育电子软件产品开发项目",
    prjName: "测试项目密码",
    prjManager: "孙工",
    prjStartDate: "2018-08-04 18:34:58",
    prjEndDate: "2018-08-28 18:34:58",
    guid: "a6d6e2d1-ea1f-47de-aec7-4397bc74bfcd",
    projectStatus: "processing",
    department: "系统管理部",
    logo: "image.png",
    taskCount: 0,
    taskDoneCount: 0,
    taskDoingCount: 0
  },
  {
    productCategory: "电话手表",
    prjCategory: "电话手表产品开发项目",
    prjName: "集成测试0712",
    prjManager: "孙工,郑工",
    prjStartDate: "2018-08-04 18:34:58",
    prjEndDate: "2018-08-28 18:34:58",
    guid: "4be3d93b-b901-462d-b87e-d17548597ab6",
    projectStatus: "processing",
    department: "系统管理部",
    logo: "image.png",
    taskCount: 0,
    taskDoneCount: 0,
    taskDoingCount: 0
  },
  {
    productCategory: "其他",
    prjCategory: "IT项目",
    prjName: "testRead",
    prjManager: "孙工",
    prjStartDate: "2018-08-06 20:56:23",
    prjEndDate: "2018-08-31 20:56:23",
    guid: "0508420c-ecc4-4cc3-9b21-3b5256874221",
    projectStatus: "approving",
    department: "系统管理部",
    logo: "image.png",
    taskCount: null,
    taskDoneCount: null,
    taskDoingCount: null
  },
  {
    productCategory: "其他",
    prjCategory: "产品预研项目",
    prjName: "任务直接完成",
    prjManager: "孙工",
    prjStartDate: "2018-07-30 16:40:03",
    prjEndDate: "2018-07-30 16:40:03",
    guid: "b4fdc9d4-dc8a-4190-b16c-d5c0f3feb379",
    projectStatus: "processing",
    department: "系统管理部",
    logo: "image.png",
    taskCount: 14,
    taskDoneCount: 13,
    taskDoingCount: 1
  },
  {
    productCategory: "其他",
    prjCategory: "测试",
    prjName: "aab1216",
    prjManager: "孙工",
    prjStartDate: "2018-07-30 16:40:03",
    prjEndDate: "2018-07-30 16:40:03",
    guid: "c6ae03d5-b90b-41da-9103-7463fa61a6f3",
    projectStatus: "processing",
    department: "系统管理部",
    logo: "image.png",
    taskCount: 1,
    taskDoneCount: 0,
    taskDoingCount: 1
  }
]);
function calculate(data) {
  data.colorShow=
  data.projectStatus === "processing" ? "blue" : "red";
  data.projectStatus =
    data.projectStatus === "processing" ? "进行中" : "审批中";
  data.show =
    data.taskCount !== null &&
    data.taskDoneCount !== null &&
    data.taskDoingCount !== null
      ? "visible"
      : "hidden";
  return data;
}
const newData = ref(data.value.map(calculate));
console.log(newData);

function clickCard() {
  show.value === 2 &&
    (([borderColor1.value, borderColor2.value] = [
      borderColor2.value,
      borderColor1.value
    ]),
    ([cardShow.value, tableShow.value] = [tableShow.value, cardShow.value]),
    (show.value = 1));
  console.log(data.value[0]);
}
function clickTable() {
  show.value === 1 &&
    (([borderColor1.value, borderColor2.value] = [
      borderColor2.value,
      borderColor1.value
    ]),
    ([cardShow.value, tableShow.value] = [tableShow.value, cardShow.value]),
    (show.value = 2));
}
</script>


<template>
<div>
  <div   class="form-top">
  <p @click="clickCard" :style="{ border:borderColor1 }">卡片</p>
  <p @click="clickTable" :style="{ border:borderColor2 }" >列表</p>
</div>
<div class="form-bottom">
<div class="card" :style="{ display:cardShow }" > 
  <div>
  <div class="item" v-for="(item,index) in newData" :key="index" >
    <img src="../../../static/images/image.jpg" alt="">
    <div class="card-text">
       <span>{{item.prjName}}<div><div></div>{{item.projectStatus}}</div> </span>
        <span>项目经理：{{item.prjManager}}</span>
        <span>立项日期：{{item.prjStartDate}}</span>
        <span :style="{visibility:item.show}">
任务：{{item.taskCount}}完成：{{item.taskDoneCount}}进行{{item.taskDoingCount}}</span>
    </div>
    <img src="../../../static/images/image.jpg" alt="">
  </div>
  </div>
  </div>
<div class="table" :style="{ display:tableShow  }" > <table>
  <thead>
    <tr >
      <th></th>
      <th>所属品类</th>
      <th>项目类别</th>
      <th>项目编号</th>
      <th>项目名称</th>
      <th>项目状态</th>
      <th>项目经理</th>
      <th>所属部门</th>
      <th>项目计划时间</th>
    </tr>
  </thead>
  <tbody>
    <tr  v-for="(item,index) in newData" :key="index" >
      <td> <img src="../../../static/images/image.jpg" alt=""></td>
      <td>{{item.productCategory}}</td>
      <td>{{item.prjCategory}}</td>
      <td></td>
      <td>{{item.prjName}}</td>
      <td><div ><div :style="{background:item.colorShow}"></div>{{item.projectStatus}} </div> </td>
      <td>{{item.prjManager}}</td>
      <td>{{item.department}}</td>
      <td>{{item.prjStartDate}}~{{item.prjEndDate}}</td>
    </tr>

  </tbody>
</table>
</div>
</div>
</div>

</template>

<style scoped>
.form-top {
  display: flex;
  justify-content: flex-end;
  font-size: 12px;
  p {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 30px;
    height: 20px;
    border: 1px solid #dcdcdc;
  }
  p:nth-child(1) {
    border-radius: 4px 0 0 4px;
  }
  p:nth-child(2) {
    border-radius: 0 4px 4px 0;
  }
}
.form-bottom {
  display: flex;
  .card {
    background-color: #fff;
    > div {
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-start;

      > div {
        margin-right: 10px;
        display: flex;
        align-items: center;
        margin-bottom: 10px;
        height: 100px;
        border: 1px solid #dadada;
        border-radius: 4px;
        box-shadow: 0.5px 0.5px 0.5px 0px rgba(218, 218, 218, 0.25);
        justify-content: space-around;
        position: relative;
        img:nth-child(1) {
          height: 40%;
          object-fit: contain;
        }
        img:nth-child(3) {
          height: 20px;
          object-fit: contain;
          position: absolute;
          bottom: 8px;
          right: 5px;
        }
        .card-text {
          text-align: start;
          font-size: 10px;
          width: 75%;
          height: 80px;
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          span:nth-child(1) {
            font-size: 14px;
            font-weight: 400;
          }
          span {
            position: relative;
            display: flex;
            justify-content: space-between;
            > div {
              height: 100%;
              position: relative;

              > div {
                position: absolute;
                background-color: #1890ff;
                width: 3px;
                border-radius: 50%;
                height: 3px;
                left: -10px;
                top: 8px;
              }
              > div::after {
                width: 3px;
                height: 3px;
                color: #1890ff;
                content: "";
                position: absolute;
                top: -1px;
                left: -1px;
                z-index: 1;
                border-radius: 50%;
                border: 1px solid rgba(24, 114, 225, 0.5);
              }
            }
          }
        }
      }
    }
  }
  .table {
    border: 1px solid #DADADA ;
    border-radius:5px;
    .item {
      width: 23%;
    }
    /* 为表格设置基本样式 */
    table {
      width: 100%; /* 表格宽度 */
      border-collapse: collapse; /* 合并边框 */
      text-align: left; /* 文本左对齐 */
    }

    /* 为表头设置样式 */
    th {
      background-color: #f2f2f2; /* 浅灰色背景 */
      color: #333; /* 深色文字 */
      padding: 10px; /* 内边距 */
    }

    /* 为表格行设置样式 */
    tr {
      border-bottom: 1px solid #ddd; /* 底部边框 */
    }

    /* 为表格单元格设置样式 */
    td {
      padding: 10px; /* 内边距 */
      border-bottom: 1px solid #ddd; /* 底部边框 */

      > div {
        display: flex;
        align-items:center;
        justify-content:space-around;
        > div {
          width: 5px;
          height: 5px;
          border-radius: 50%;
        }
      }
        >img {
    height: 15px;
    margin-left: 48%;
  }
    }

    /* 为奇数行设置不同的背景色 */
    tr:nth-child(odd) {
      background-color: #f9f9f9; /* 浅灰色背景 */
    }

    /* 为鼠标悬停的行设置样式 */
    tr:hover {
      background-color: #f1f1f1; /* 浅灰色背景 */
    }
  }

}
@media (max-width: 600px) {
  .item {
    width: 98%;
  }
}
@media (min-width: 600px) and (max-width: 900px) {
  .item {
    width: 48%;
  }
}
@media (min-width: 900px) and (max-width: 1200px) {
  .item {
    width: 31%;
  }
}
@media (min-width: 1200px) {
}
</style>
