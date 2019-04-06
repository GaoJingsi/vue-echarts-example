<template>
  <div id="app">
    <el-container>


      <el-menu default-active="1-4-1" class="el-menu-vertical" :collapse="isCollapse" :collapse-transition="false"
               :router="true" :unique-opened="true">

        <el-submenu v-for="(item,index) in navData" :index="index.toString()">
          <template slot="title">
            <i :class="item.styleClass"></i>
            <span slot="title">{{item.navText}}</span>
          </template>
          <el-menu-item-group v-for="(group,groupIndex) in item.groups">
            <span slot="title">{{group.groupText}}</span>
            <el-menu-item :index="menu.menuPath" v-for="(menu,menuIndex) in group.menus">{{menu.menuText}}
            </el-menu-item>
          </el-menu-item-group>
        </el-submenu>

      </el-menu>


      <el-container>
        <el-header class="header">

          <el-row>
            <el-col :span="12">
              <el-button @click="collapseOrExpand" class="collapseOrExpandBtn el-icon-menu"></el-button>
            </el-col>

            <el-col :span="12" class="rightInfo">
              <el-dropdown>
              <span class="el-dropdown-link">
                下拉菜单<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
                <el-dropdown-menu slot="dropdown">
                  <el-dropdown-item>黄金糕</el-dropdown-item>
                  <el-dropdown-item>狮子头</el-dropdown-item>
                  <el-dropdown-item>螺蛳粉</el-dropdown-item>
                  <el-dropdown-item disabled>双皮奶</el-dropdown-item>
                  <el-dropdown-item divided>蚵仔煎</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>
            </el-col>
          </el-row>

        </el-header>
        <el-main>
          <router-view/>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        //样式数据
        isCollapse: false,
        //  后台数据
        navData: [
          {
            styleClass: 'el-icon-document',
            navText: '导航1',
            groups: [
              {
                groupText: '组1',
                menus: [
                  {
                    menuText: '菜单2',
                    menuPath: '/'
                  },
                  {
                    menuText: '菜单2',
                    menuPath: '/HelloWorld2'
                  }
                ]
              }
            ]
          },
          {
            styleClass: 'el-icon-location',
            navText: '导航2',
            navPath: '/HelloWorld2',
            groups: [
              {
                groupText: '组2',
                menus: [
                  {
                    menuText: '菜单2',
                    menuPath: '/'
                  },
                  {
                    menuText: '菜单2',
                    menuPath: '/HelloWorld2'
                  }
                ]
              }
            ]
          },
          {
            styleClass: 'el-icon-setting',
            navText: '导航3',
            navPath: '/HelloWorld2',
            groups: [
              {
                groupText: '组3',
                menus: [
                  {
                    menuText: '菜单3',
                    menuPath: '/'
                  },
                  {
                    menuText: '菜单3',
                    menuPath: '/HelloWorld2'
                  }
                ]
              },{
                groupText: '组4',
                menus: [
                  {
                    menuText: '菜单4',
                    menuPath: '/'
                  },
                  {
                    menuText: '菜单4',
                    menuPath: '/HelloWorld2'
                  }
                ]
              }
            ]
          }
        ]
      };
    },
    methods: {
      collapseOrExpand() {
        this.isCollapse = !this.isCollapse;
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }

  html, body, #app, #app > .el-container {
    width: 100%;
    height: 100%;
  }

  #app > .el-container > .el-aside {
    background-color: deepskyblue;
  }

  .header {
    line-height: 60px;
    height: 60px;
    border-bottom: solid 1px #e6e6e6;
  }

  .el-menu-vertical {
    overflow-y: auto;
    overflow-x: hidden;
  }

  .el-menu-vertical:not(.el-menu--collapse) {
    width: 200px;
  }

  .collapseOrExpandBtn {

  }

  .rightInfo {
    text-align: right;
  }

  .rightInfo .el-dropdown-link {
    cursor: pointer;
  }

  .el-icon-arrow-down {
    font-size: 12px;
  }
</style>
