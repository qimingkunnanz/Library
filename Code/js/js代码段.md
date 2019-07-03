### js相关

1. 截取url地址中的参数

   ```javascript
   // url表示地址栏的字符串， name表示要获取的对应的key
   function getParamsByUrl(url, name) {
   	var params = url.substr(url.indexOf('?')+1);
   	var param = params.split('&');
   	for(var i=0;i<param.length;i++){
   		var current = param[i].split('=');
   		if(current[0] == name){
   			return current[1]
   		}
   	}
   	return null;
   }
   ```

2. 快速排序

   ```js
   var tmpArr = [];
   for(var i =0;i<10000;i++){
     tmpArr.push(Math.floor(Math.random()*10001)) //随机生成0-1000的随机数
   }
   
   function quickSort(arr, left, right) {
     var len = arr.length,
         partitionIndex,
         left = typeof left != 'number' ? 0 : left,
         right = typeof right != 'number' ? len - 1 : right;
   
     if (left < right) {
         partitionIndex = partition(arr, left, right);
         quickSort(arr, left, partitionIndex-1);
         quickSort(arr, partitionIndex+1, right);
     }
     return arr;
   }
   
   function partition(arr, left ,right) {     // 分区操作
     var pivot = left,                      // 设定基准值（pivot）
         index = pivot + 1;
     for (var i = index; i <= right; i++) {
         if (arr[i] < arr[pivot]) {
             swap(arr, i, index);
             index++;
         }        
     }
     swap(arr, pivot, index - 1);
     return index-1;
   }
   
   function swap(arr, i, j) {
     var temp = arr[i];
     arr[i] = arr[j];
     arr[j] = temp;
   }
   
   console.time('1')
   console.log(quickSort(tmpArr));
   
   console.timeEnd('1')
   ```

3. 遍历数组

   ```
   let arr=[11,223,45,78];
   
   ```

   