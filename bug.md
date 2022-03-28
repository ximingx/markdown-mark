# git

## git clone > HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

```bash
> git clone https://github.com/ximingx/markdown-mark.git

Cloning into 'markdown-mark'...
fatal: unable to access 'https://github.com/ximingx/markdown-mark.git/': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

> git config --global http.version HTTP/1.1
> git clone https://github.com/ximingx/markdown-mark.git
```

