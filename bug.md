# git

## git clone > HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

```bash
> git clone https://github.com/ximingx/markdown-mark.git

Cloning into 'markdown-mark'...
fatal: unable to access 'https://github.com/ximingx/markdown-mark.git/': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

> git config --global http.version HTTP/1.1
> git clone https://github.com/ximingx/markdown-mark.git
```

## git push > error: failed to push some refs to 'github.com:ximingx/markdown-mark.git'

```bash
> git push

To github.com:ximingx/markdown-mark.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:ximingx/markdown-mark.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

> git 提交冲突,远端代码与本地代码不一致（别人在你提交之前提交了代码，导致你本地现在的代码与远端现在的代码不一致。）
> 将自己新写的代码备份到其他地方。
> 删除本地项目里自己新写的代码。
> git pull 下拉代码，使本地代码与远端代码一致。
> 重新上传代码 
> git add .
> git commit -m "fix bug"
> git push
```

切记：下班前 push 代码，上班后第一件事要 pull 代码

