# SSH免密

```
cd ~
ssh-keygen -t -rsa -C [GitHub账号]
cd .ssh/
cat id_rsa.pub    # copy内容
```

- 选择settings – SSH and GPG  – ADD SSH

- 进入工作区

  ```
  git remote add [ssh别名] [SSHd]
  git remote -v    # 查看
  ```

  

