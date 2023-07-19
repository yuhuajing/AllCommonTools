# 初始化golang项目

## 单包文件
> https://github.com/yuhuajing/AllCommonTools/tree/main/golang/helloWorldSinglePack
所有函数都定义在main.go中，只需要在文件夹下执行```go mod init main``` +  ```go mod tidy``` 创建golang的可执行环境即可

## 面向对象的分包操作
> https://github.com/yuhuajing/AllCommonTools/tree/main/golang/helloWorldMultiPack
分包文件的package名称必须和当前路径下的文件名保持一致，并且只有外部包内的首字母大写的函数、变量才能被别的包导入使用。

在main.go文件中，直接输入package(包名)调用首字母大写的函数或变量即可。

如果报错找不到包，那就先删除本地的```rm -rf go.mod``` 然后重新生成即可```go mod init main``` +  ```go mod tidy```