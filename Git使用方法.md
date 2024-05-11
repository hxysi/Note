## 将本地项目推送到远程仓库

### 常用方法

删除本地的 .git 目录来取消Git跟踪

```bash
rm -rf .git
```

从远程仓库拉取

```bash
git pull origin master
```

切换分支

```bash
git checkout 分支名
```

查看提交历史

```bash
git log
```

查看当前目录下的文件

```bash
ls -l
```

查看提交状态

```bash
git status
```

恢复删除的文件

```bash
git restore .
```

删除文件

```bash
rm 文件名
```


---

**如果你是用的远程仓库不是Github，那么你可以直接跳到：**[这里](#Nogithub)

---

1. 查看C盘中的用户文件夹里是否存在.ssh文件夹
<img width="690" alt="ssh" src="https://github.com/LHXTechie/Note/assets/61722590/da2cac3e-3fa8-4261-a488-1c1967a0d8c2">

> [!TIP]
>
> 如果没有，则创建一个.ssh文件夹

2. 查看.ssh文件夹中是否有 `id_esa` 和 `id_rsa.pub` 这两个文件。这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。
<img width="703" alt="sshFile" src="https://github.com/LHXTechie/Note/assets/61722590/0e3dd936-4598-4f78-bb1f-23a8e40377e0">

> [!tip]
>
> 如果没有这个文件，那么以管理员身份打开 ***GitBash*** ，输入以下命令
>
> ```bash
> $ ssh-keygen -t rsa -C "youremail@example.com"
> ```
>
> 一路回车即可。

3. **登录Github** > Settings > **SSH andGPG keys** > **New SSH Key** ，接着以文本形式打开 `id_rsa.pub` 文件，将里面的内容复制进来，Title可以随意填写。点击完成。

<a id="Nogithub">没有使用Github，直接从这里开始</a>

1. 切换到项目目录

```bash
cd "your/path"
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
git remote add origin http://gitee.com/your_remote_warehous.git
```

> [!tip]
>
> 可以通过命令来测试远程仓库是否连接成功
>
> ```bash
> git remote -v
> ```

6. 防止推送失败，先将项目目录添加到安全例外

```bash
git config --global --add safe.directory "D:/your/path"
```

7. 尝试推送

```bash
git push -u origin master
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
git push -u origin master
```

推送完毕，查看远程仓库。





