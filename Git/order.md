一. 删除分支
>git push origin --delete master

二. 上传本地项目到Github
1. 在Github上创建一个新的仓库,不要勾选Initialize this repository with a README
2. 在本地项目的控制台执行：
```git
echo "# batchTransfer" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/xxx/xxx.git
git push -u origin main
```
