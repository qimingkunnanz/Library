### vue报错集合

1. Unknown custom element: <router-view> - did you register the component correctly? For recursive components, make sure to provide the "name" option

   没有添加 ` Vue.use(VueRouter) ` 

2. 使用mint ui 写轮播图 不显示
   1. 可能是没有设置高
   2. 可能是没有写样式
   3. 不轮播 没有加js

3. bundle.js:2081 [Vue warn]: Duplicate keys detected: 'http://www.itcast.cn/subject/phoneweb/index.html'. This may cause an update error

   1. 使用 v-for 的 :key值不唯一

