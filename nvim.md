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
| <C\-d>     | :BD              | 删除缓冲区                                 | <++> |
| <++>     | <++>              | <++>                                 | <++> |
| <++>     | <++>              | <++>                                 | <++> |

```vim
" 设置<C-i>, <C-k>上下移动
" 在.zshrc/.bashrc中设置
export FZF_DEFAULT_OPTS="--bind ctrl-k:down,ctrl-i:up"

也可以直接在init.vim中设置
let g:fzf_bind = {'ctrl-k':'down', 'ctrl-i':'up'}
```

#### Leaderf
| shortcut | motions     |
|----------|-------------|
| <C\-p>   | 打开Leaderf |
以下命令基于Leaderf已打开
copy from [https://github.com/Yggdroot/LeaderF](https://github.com/Yggdroot/LeaderF) 
| Command                    | Description
| -------                    | -----------
| `<C-C>`<br>`<ESC>`         | quit from LeaderF
| `<C-R>`                    | switch between fuzzy search mode and regex mode
| `<C-F>`                    | switch between full path search mode and name only search mode
| `<Tab>`                    | switch to normal mode
| `<C-V>`<br>`<S-Insert>`    | paste from clipboard
| `<C-U>`                    | clear the prompt
| `<C-W>`                    | delete the word before the cursor in the prompt
| `<C-J>`                    | move the cursor downward in the result window
| `<C-K>`                    | move the cursor upward in the result window
| `<Up>`/`<Down>`            | recall last/next input pattern from history
| `<2-LeftMouse>`<br>`<CR>`  | open the file under cursor or selected(when multiple files are selected)
| `<C-X>`                    | open in horizontal split window
| `<C-]>`                    | open in vertical split window
| `<C-T>`                    | open in new tabpage
| `<C-\>`                    | show a prompt enable to choose split window method: vertical, horizontal, tabpage, etc
| `<F5>`                     | refresh the cache
| `<C-LeftMouse>`<br>`<C-S>` | select multiple files
| `<S-LeftMouse>`            | select consecutive multiple files
| `<C-A>`                    | select all files
| `<C-L>`                    | clear all selections
| `<BS>`                     | delete the preceding character in the prompt
| `<Del>`                    | delete the current character in the prompt
| `<Home>`                   | move the cursor to the begin of the prompt
| `<End>`                    | move the cursor to the end of the prompt
| `<Left>`                   | move the cursor one character to the left in the prompt
| `<Right>`                  | move the cursor one character to the right in the prompt
| `<C-P>`                    | preview the result
| `<C-Up>`                   | scroll up in the popup preview window
| `<C-Down>`                 | scroll down in the popup preview window

#### vim-visual-multi
| shortcut           | motions            |
|--------------------|--------------------|
| <C\-k>             | 打开选中模式并选中 |
| :help visual-multi | 查看文档           |
| :h vm-mappings.txt | 查看映射文档       |

以下命令基于visual-multi已打开
| shortcut | motions    |
|----------|------------|
| k        | 向下移动   |
| i        | 向上移动   |
| j        | 向左移动   |
| l        | 向右移动   |
| =        | 下一个     |
| -        | 上一个     |
| q        | 取消该选中 |
| <C\-n>   | 跳过选中   |
| <++>     | <++>       |

#### Far.vim(TODO)
跨文件查找替换
```vim
" 查找替换
:Far {pattern} {replace-with} {file-mask} [params]
" 仅查找
:F {pattern} {file-mask} [params]
" 执行替换操作
:Fardo
```
| shortcut | motions    |
|----------|------------|
| LEADER+f | 跨文件查找 |
| <++>     | <++>       |

#### Bullets.vim(TODO)
<++>

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

#### function
```vim
fu[nction][!] {name}([arguments]) [range] [abort] [dict] [closure]
" name必须以字母数字或_开头, 开头必须大写或以s:开头
" s:表示局部变量
```

```vim
redir 重定向
redir > {file} "重定向到file
redir! > {file} "强制覆盖file
redir >> {file} "追加
redir END "结束重定向

" 返回缓冲区列表的函数
function! s:list_buffers()
  redir => list
  silent ls
  redir END
  return split(list, "\n")
endfunction

" 删除一个buffer
function! s:delete_buffers(lines)
  execute 'bwipeout' join(map(a:lines, {_, line -> split(line)[0]}))
endfunction

" 定义命令行调用函数function
" :BD调用
command! BD call function

```





