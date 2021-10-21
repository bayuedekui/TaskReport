<template>
  <div>
    <a-row type="flex" justify="center" align="top">
      <a-col :span="16">
        <a-input-search placeholder="input your task" size="default" v-model="taskInfo" @search="publish">
          <a-icon slot="prefix" type="edit"/>
          <a-button slot="enterButton">
            发布
          </a-button>
        </a-input-search>
        <span> </span>

<!--        <a-list item-layout="horizontal" :data-source="taskContainer">
          <a-list-item slot="renderItem" slot-scope="item,index">

            <a-popover v-model="visible" trigger="click" slot="actions">
              <a slot="content" @click="hide"> 编辑 </a>
              <a slot="content" @click="hide">&nbsp;100% </a>
              <a slot="content" @click="hide">&nbsp;50% </a>
              <a slot="content" @click="hide">&nbsp;0% </a>
              <a slot="content" @click="hide">&nbsp;备注 </a>
              <a-icon type="form" size="large" />
            </a-popover>
            <a-list-item-meta :description="item.comments">
              <h2 slot="title" >{{ item.idx }}</h2>
              <h2 slot="title" >{{ item.title }}</h2>
&lt;!&ndash;              <a-avatar
                  slot="avatar"
                  src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"
              />&ndash;&gt;
            </a-list-item-meta>
          </a-list-item>
        </a-list>-->
        <a-table :columns="columns" :data-source="data" class="components-table-demo-nested">
          <a slot="operation" slot-scope="text">Publish</a>
          <a-table
              slot="expandedRowRender"
              slot-scope="text"
              :columns="innerColumns"
              :data-source="innerData"
              :pagination="false"
          >
            <span slot="status" slot-scope="text"> <a-badge status="success" />Finished </span>
            <span slot="operation" slot-scope="text" class="table-operation">
        <a>Pause</a>
        <a>Stop</a>
        <a-dropdown>
          <a-menu slot="overlay">
            <a-menu-item>
              Action 1
            </a-menu-item>
            <a-menu-item>
              Action 2
            </a-menu-item>
          </a-menu>
          <a> More <a-icon type="down" /> </a>
        </a-dropdown>
      </span>
          </a-table>
        </a-table>
      </a-col>
    </a-row>
  </div>
</template>

<script>
// const taskContainer = [
//   {
//     title: 'Ant Design Title 1',
//     comments: 'caonima1'
//   },
//   {
//     title: 'Ant Design Title 2',
//     comments: 'caonima2'
//   },
//   {
//     title: 'Ant Design Title 3',
//     comments: 'caonima3'
//   },
//   {
//     title: 'Ant Design Title 4',
//     comments: 'caonima4'
//   },
// ];
const columns = [
  { title: 'Name', dataIndex: 'name', key: 'name' },
  { title: 'Platform', dataIndex: 'platform', key: 'platform' },
  { title: 'Version', dataIndex: 'version', key: 'version' },
  { title: 'Upgraded', dataIndex: 'upgradeNum', key: 'upgradeNum' },
  { title: 'Creator', dataIndex: 'creator', key: 'creator' },
  { title: 'Date', dataIndex: 'createdAt', key: 'createdAt' },
  { title: 'Action', key: 'operation', scopedSlots: { customRender: 'operation' } },
];

const data = [];
for (let i = 0; i < 3; ++i) {
  data.push({
    key: i,
    name: 'Screem',
    platform: 'iOS',
    version: '10.3.4.5654',
    upgradeNum: 500,
    creator: 'Jack',
    createdAt: '2014-12-24 23:12:00',
  });
}

const innerColumns = [
  { title: 'Date', dataIndex: 'date', key: 'date' },
  { title: 'Name', dataIndex: 'name', key: 'name' },
  { title: 'Status', key: 'state', scopedSlots: { customRender: 'status' } },
  { title: 'Upgrade Status', dataIndex: 'upgradeNum', key: 'upgradeNum' },
  {
    title: 'Action',
    dataIndex: 'operation',
    key: 'operation',
    scopedSlots: { customRender: 'operation' },
  },
];

const innerData = [];
for (let i = 0; i < 3; ++i) {
  innerData.push({
    key: i,
    date: '2014-12-24 23:12:00',
    name: 'This is production name',
    upgradeNum: 'Upgraded: 56',
  });
}

export default {
  name: "TaskReport",
  props: {},
  data() {
    return {
      data,
      columns,
      innerColumns,
      innerData,
      visible: false,
      taskInfo: '',
      taskContainer:[],
    }
  },
  methods: {
    publish() {
      this.$message.info(this.taskContainer.length)
      let tmpTask={}
      tmpTask.idx=this.taskContainer.length+1
      tmpTask.title=this.taskInfo
      tmpTask.comments='null'
      this.taskContainer.push(tmpTask)
      this.taskInfo=null
    },
    hide() {
      this.visible = false;
    },
  },
}

</script>

<style scoped>

</style>