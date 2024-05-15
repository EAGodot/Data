# md語法
## 無序列表
* 1
## 有序列表
1. 1
## 區塊引用
* 引用説明
  >内容來自：https://www.cnblogs.com/cqczx/articles/13410096.html
  >>引用嵌套
## 分割綫
* * *
分割线可以由* - _（星号，减号，底线）这3个符号的至少3个符号表示，注意至少要3个，且不需要连续，有空格也可以
_ _ _ _
## 鏈接
[網址1](www.baidu.com)
*[網址2](www.baidu.com)
## 圖片
![圖片1](圖片地址)
[圖片2]:(圖片地址)
## 代碼框
`
devices_init(); 
`
```可以寫注釋
void __init driver_init(void)
{
  /* These are the core pieces */
  //创建tmpfs文件夹
  devtmpfs_init(); 
  //创建devices ，dev文件夹                
  devices_init(); 
  //创建bus文件夹                 
  buses_init();     
  //创建class文件夹       
  classes_init();             
  firmware_init();
  hypervisor_init();
  /* These are also core pieces, but must come after the
   * core core pieces.
   */
  //创建platformbus文件夹
  platform_bus_init();            
  system_bus_init();
  cpu_dev_init();
  memory_dev_init();
}
```
## 表格
看參考鏈接
## 强調
*字體傾斜* _字體傾斜_ **字體加粗** __字體加粗__
## 轉義
看參考鏈接
## 刪除綫
~~刪除了~~
