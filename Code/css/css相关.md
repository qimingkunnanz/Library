### css相关

1. 清除浮动

   ```css
   .clearfix::after { /*伪元素*/
     display: block;
     clear: both;
     content: "";
   }
   
   <p class="clearfix">
   ```

2. 响应式布局,媒体查询(学习bootstarp的)

   ```css
   /*这是bootstarp4响应式布局书写*/
   @media (min-width: 768px){
     .col-md-1 {
       -ms-flex: 0 0 8.333333%;
       flex: 0 0 8.333333%;
       max-width: 8.333333%;
     }
   }
   /*这是bootstarp3响应式布局书写*/
   @media (min-width: 768px){
     .col-md-1 {
       float:left;
       width: 8.33333%;
     }
   }
   ```

3. btn按钮样式的书写

   ```css
   .btn {
     display: inline-block;
     font-weight: 400;
     color: #212529;
     text-align: center;
     vertical-align: middle;
     -webkit-user-select: none;
     -moz-user-select: none;
     -ms-user-select: none;
     user-select: none;
     background-color: transparent;
     border: 1px solid transparent;
     padding: 0.375rem 0.75rem;
     font-size: 1rem;
     line-height: 1.5;
     border-radius: 0.25rem;
     transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
   }
   ```

4. mui清除浮动框架

   ```css
   .mui-clearfix:before, .mui-clearfix:after
   {
       display: table;
   
       content: ' ';
   }
   .mui-clearfix:after
   {
       clear: both;
   }
   ```

5. 浮动

   ```css
   .mui-pull-left
   {
       float: left;
   }
   
   .mui-pull-right
   {
       float: right;
   }
   ```

