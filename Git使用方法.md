## 将本地项目推送到远程仓库

1. 切换到项目目录

```bash
cd "D:/C#/winforms/study1/studywinform"
```

2. 初始化仓库

`````bash
git init
`````

3. 将项目添加到仓库中

```bash
git add .
```

4. 提交

```bash
git commit -m "提交说明"
```

5. 连接远程仓库

```bash
git remote add origin http://gitee.com/lhxHb/test-winform.git
```

6. 防止推送失败，先将项目目录添加到安全例外

```bash
git config --global --add safe.directory "D:/c#/winForms/study1/studywinform"
```

7. 尝试推送

```bash
git pull origin master
```

> [!tip]
>
> 如果此时推送失败，那么进行以下操作：
>
> ```bash
> git pull origin master --allow-unrelated-histories
> ```

执行完这条命令，会打开文本编辑器，删除文本编辑器中的带有`#`的注释部分。保存文本文档并关闭。

8. 再次尝试推送

```bash
git pull origin master
```

推送完毕，查看远程仓库。





