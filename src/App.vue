<template>
  <div id="app">
    <nav class="navbar navbar-default">
      <div class="container-fluid">
       <ul class="nav navbar-nav">
          <li>
            <router-link to="/">Home</router-link>
          </li>
           <li>
            <router-link to="/createcourse">Create Course</router-link>
          </li>
          <!-- <li>
            <router-link to="/applicationform">Application Form</router-link>
          </li> -->
          <li>
            <router-link to="/myapplications">Student Read</router-link>
          </li>
           <li>
            <router-link to="/adminread">Admin Read</router-link>
          </li>
          <li>
            <router-link to="/adminmanage">Admin Manage</router-link>
          </li>
        </ul>
      </div>
    </nav>
    <router-view class="view"></router-view>
  </div>
</template>

<script>
import Vue from "vue";
import VueRouter from "vue-router";
import Oruga from '@oruga-ui/oruga'
import ElementUI from 'element-ui';

import "bootstrap/dist/css/bootstrap.css";
import "element-ui/lib/theme-chalk/index.css"
import '@oruga-ui/oruga/dist/oruga.css'

Vue.use(ElementUI);
Vue.use(Oruga);
Vue.use(VueRouter);

const Home = () => import("./views/Home.vue");
const CreateCourse = () =>
  import(/* webpackChunkName: "createcourse" */ "./views/CreateCourse.vue");
const ApplicationForm = () =>
  import(/* webpackChunkName: "applicationform" */ "./views/ApplicationForm.vue");
const MyApplications = () =>
  import(/* webpackChunkName: "myapplications" */ "./views/MyApplications.vue");
  const AdminRead = () =>
  import(/* webpackChunkName: "adminread" */ "./views/AdminRead.vue");
   const AdminManage = () =>
  import(/* webpackChunkName: "adminmanage" */ "./views/AdminManage.vue");
const ExportToPDF = () =>
  import(/* webpackChunkName: "creator" */ "./views/ExportToPDF.vue");
const Analytics = () =>
  import(/* webpackChunkName: "creator" */ "./views/Analytics.vue");
const AnalyticsTabulator = () =>
  import(/* webpackChunkName: "creator" */ "./views/AnalyticsTabulator.vue");
const AnalyticsDatatables = () =>
  import(/* webpackChunkName: "creator" */ "./views/AnalyticsDatatables.vue");

const router = new VueRouter({
  mode: "history",
  base: __dirname,
  routes: [
    { path: "/", component: Home },
    { path: "/createcourse", component: CreateCourse },
    // Just use them normally in the route config
    { path: "/applicationform/:id", component: ApplicationForm },
    // multiple parameters, `/` should not be encoded. The name is also important
    // https://github.com/vuejs/vue-router/issues/2719
    // { path: '/a/:tags*', name: 'tagged', component: () => new Promise(resolve => {
    //   setTimeout(() => {
    //     resolve({
    //       template: `<div>
    //         <h2>Lazy with params</h2>
    //         <pre id="tagged-path">{{ $route.path }}</pre>
    //       </div>`
    //     })
    //   }, 200)
    // }) },
    // Bar and Baz belong to the same root route
    // and grouped in the same async chunk.
    { path: "/myapplications", component: MyApplications },
    { path: "/adminread", component: AdminRead },
    { path: "/adminmanage", component: AdminManage },
    { path: "/exportpdf", component: ExportToPDF },
    { path: "/analytics", component: Analytics },
    { path: "/analyticstabulator", component: AnalyticsTabulator },
    { path: "/analyticsdatatables", component: AnalyticsDatatables },
  ],
});

export default {
  name: "app",
  router: router,
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
