| shortcut   | command             | motions          | mode |
|------------|---------------------|------------------|------|
| Y          | y$                  | 复制到行尾       | n    |
| Y          | "+y                 | 复制到系统剪切板 | v    |
| <LEADER>dw | /\(\<\w\+\>\)\_s*\1 | 找到邻近的重复词 |      |
| <LEADER>tt | :%s/    /\t/g       | 使用tab代替空格     | n    |
| <LEADER>tt | :s/    /\t/g        | 使用tab代替空格     | v    |
| <LEADER>o  | za                  | 折叠             | <++> |
| <++>       | <++>                | <++>             | <++> |
| <++>       | <++>                | <++>             | <++> |
| <++>       | <++>                | <++>             | <++> |
| <++>       | <++>                | <++>             | <++> |
| <++>       | <++>                | <++>             | <++> |


Command Mode

| shortcut | command      | motions |
|----------|--------------|---------|
| <C\-a>   | \<Home\>     | <++>    |
| <C\-e>   | \<End\>      | <++>    |
| <C\-i>   | \<Up\>       | <++>    |
| <C\-k>   | \<Down\>     | <++>    |
| <C\-j>   | \<Left\>     | <++>    |
| <C\-l>   | \<Right\>    | <++>    |
| <M\-b>   | \<S\-Left\>  | <++>    |
| <M\-w>   | \<S\-Right\> | <++>    |

#### Window management
| shortcut | command        | motions                  | mode |
|----------|----------------|--------------------------|------|
| LEADER+w | <C\-w>w        | 回到上一个窗口           | <++> |
| qf       | <C\-w>o        | 关闭其他窗口             | <++> |
| sh       | <C\-w>t<C\-w>K | 切换窗口划分，左右->上下 | <++> |
| sv       | <C\-w>k<C\-w>H | 切换窗口划分，上下->左右 | <++> |
| LEADER+q | <C\-w>j:q<CR>  | 关闭当前窗口前一个窗口   | <++> |
| <++>     | <++>           | <++>                     | <++> |
| <++>     | <++>           | <++>                     | <++> |

#### Tab management
| shortcut | command       | motions             | mode |
|----------|---------------|---------------------|------|
| tmj      | :-tabmove<CR> | 向前移动该tab的位置 | <++> |
| tml      | :+tabmove<CR> | 向后移动该tab的位置 | <++> |
| <++>     | <++>          | <++>                | <++> |
| <++>     | <++>          | <++>                | <++> |
| <++>     | <++>          | <++>                | <++> |

#### Markdown
| shortcut | command | motions | mode |
|----------|---------|---------|------|
| <++>     | <++>    | <++>    | <++> |
| <++>     | <++>    | <++>    | <++> |
| <++>     | <++>    | <++>    | <++> |

| command                                         | motions                                          |
|-------------------------------------------------|--------------------------------------------------|
| autocmd BufRead,BufNewFile \*.md setlocal spell | 自动设置读取md文件和创建新md文件时, 设置拼写检查 |


#### Others
| shortcut      | command                                            | motions                                   | mode |
|---------------|----------------------------------------------------|-------------------------------------------|------|
| <++>          | :term sh -c 'st'                                   | terminal执行st命令                        | <++> |
| LEADER+/      | :set splitbelow<CR>:split<CR>:res +10<CR>:term<CR> | 在下方打开terminal                        | <++> |
| LEADER+LEADER | <Esc>/<++><CR>:nohlsearch<CR>c4l                   | 找到下一个<++>并替换进入插入模式          | <++> |
| <++>          | <++>                                               | <++>                                      | <++> |
| LEADER+sc     | :set spell!<CR>                                    | 设置拼写检查                              | <++> |
| tx            | :r !figlet                                         | 写入艺术字                                | <++> |
| LEADER+sw     | :set wrap<CR>                                      | 设置自动折行,多行显示单行，但不添加换行符 | <++> |
| <F10>         | :call SynGroup()<CR>                               | 显示高亮                                  | <++> |
| LEADER+B      | :call BufCloseOthers()<CR>                         | 关闭其他缓冲区，仅保留当前缓冲区          | <++> |
| r             | :call CompileRunGcc()<CR>                          | 执行文件                                  | <++> |
| <++>          | <++>                                               | <++>                                      | <++> |
| <++>          | <++>                                               | <++>                                      | <++> |

#### GitGutter
| shortcut  | command                | motions                | mode |
|-----------|------------------------|------------------------|------|
| LEADER+gf | :GitGutterFold<CR>     | 遮挡未修改的地方       | <++> |
| LEADER+g- | :GitGutterPrevHunk<CR> | 跳转到上一个修改的地方 | <++> |
| LEADER+g= | :GitGutterNextHunk<CR> | 跳转到下一个修改的地方 | <++> |
| <++>      | <++>                   | <++>                   | <++> |
| <++>      | <++>                   | <++>                   | <++> |

| command                              | motions                                      |
|--------------------------------------|----------------------------------------------|
| autocmd BufEnter * silent! lcd %:p:h | 自动设置进入缓冲区时切换为当前文件所在文件夹 |


#### coc-nvim(TODO)
```vim
" pumvisible()表示是否有补全列表
" 函数表示如果有补全列表则执行<C\->p, 否则执行<C\-h>
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"
```
| shortcut | command                        | motions            | mode |
|----------|--------------------------------|--------------------|------|
| LEADER+h | :call Show_documentation()<CR> | 查看光标所在处文档 | n    |
| <++>     | <++>                           | <++>               | <++> |
| <++>     | <++>                           | <++>               | <++> |
| <++>     | <++>                           | <++>               | <++> |

#### FZF
需要安装fzf和fzf.vim
| shortcut | command           | motions                              | mode |
|----------|-------------------|--------------------------------------|------|
| <C\-p>   | :Leaderf file<CR> | 查找该文件所在文件夹下的文件         | n    |
| <C\-f>   | :Rg<CR>           | 在该文件夹下查找，可通过文件内容查找 | <++> |
| <C\-h>   | :History<CR>      | 根据历史查找                         | <++> |
| <C\w>    | :Buffers<CR>      | 查找缓冲区                           | <++> |
| LEADER+; | :History:<CR>     | 命令行的历史                        | <++> |
| <++>     | <++>              | <++>                                 | <++> |

```vim
" 设置<C-i>, <C-k>上下移动
" 在.zshrc/.bashrc中设置
export FZF_DEFAULT_OPTS="--bind ctrl-k:down,ctrl-i:up"

也可以直接在init.vim中设置
let g:fzf_bind = {'ctrl-k':'down', 'ctrl-i':'up'}
```


#### autocmd
:autocmd [group] events pattern [nested] command
- group，组名是可选项，用于分组管理多条自动命令；
- events，事件参数，用于指明触发命令的一个或多个事件；
- pattern，限定针对符合匹配模式的文件执行命令；
- nested，嵌套标记是可选项，用于允许嵌套自动命令；
- command，指明需要执行的命令、函数或脚本。
![autocmd](./imgs/autocmd.jpg) 

:autocmd FileWritePre * :callDateInsert()<CR>
在保存文件的时候自动执行函数callDateInsert()
