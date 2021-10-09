# esc 命令模式切换

在大多数编辑器中，相信大家都喜欢敲几个单词就“保存（ctrl+s）”一下。而在vim中，保存是`:w`，而且需要在命令模式下进行。因此，往往要按`Esc:w`多达三个键才能保存。很多初学者十分诟病这个设计。事实上，经常使用`Esc`切换到命令模式才是vimer需要练就的第一个重要的反射行为。可以毫不夸张的说，只要你不在输入文字，就应该切换在命令模式下，命令模式应该是常态！

# hjkl

h 向前移动一个字符

j 向下移动一行

k 向上移动一行

l 向后移动一个字符

# 光标移动

- `w`、`e`、`b`：按照单词进行前后光标跳转，也可以组合数字进行跳转，不过以我的经验，与其去算要跳多少个单词，不如多按几次吧。
- `I`、`A`：移动到行首或行末的第一个字符处，并进入插入模式。
- `H`、`M`、`L`：光标分别跳转到可视区域的最上面、中间、最下面。
- `Ctrl+D`、`Ctrl+U`：有时，需要看的文本不在可视区域，通过这些组合进行上下翻页。
- `^`、`$`、`0`：光标移动到行首和行尾（0是绝对行首）。不过因为`^`和`$`都需要同时按住shift，而且数字键我们往往难以盲打，** 所以我一般直接使用`I+Esc`、`A+Esc`。**
- `%`：移动到与当前括号匹配的括号处。
- `f`、`F`：通过上面的例子，我们知道，`f`是find的意思，可以在一行内查找某个字符出现的位置，并直接跳转过去。比如`f<`可以从当前光标开始向右，找到第一个`<`，并移动过去。F是向左查找。

# 插入

* `i` 、`a` : 都为从命令模式进入编辑模式，区别为`i`退出命令模式后会向前前进一个字符，`a`不会
* `I`、`A`：移动到行首或行末的第一个字符处，并进入编辑模式。
* `O`、`o` `O`在当前行上方新建一行，并进入编辑模式，`o`在当前行下方新建一行，进入编辑模式。

# 删除

* `dd`: 删除当前光标所在的一行
* `dw`: 删除一个单词
* `x` :  删除当前光标覆盖的字符
* `X`、`D`: 删除光标前的字符

# 撤销
`u`: 撤销上一次输入
`Ctrl+r` 回退前一个命令（即还原上次撤销）

# 复制

* `nyy`: 复制n行
* `yy`、`Y`: 复制当前行

# 高效修改

- `r`：替换模式，替换当前光标所在位置的一个字符。虽然你同样可以`i`进入插入模式，然后删掉那个字符，再输入需要的字符，但这种操作是鼠标流思维方式。替换是一个可重复操作，多用没坏处。
- `cw`：`change word`可以删除从当前位置到一个单词的结尾，并进入插入模式。这种操作常用于修改一个变量。比如对于：`int count=0;`希望把`count`改成`cnt`，那么当光标位于`c`字符处的时候，按`cw`可直接删除`count`，并进入插入模式。然后直接继续输入`cnt`即可。
- `caw`：`change a word`可以删除当前光标所在位置的单词。对于`int count=0;`的例子，如果此时光标在`count`中间某处，比如`u`处，直接键入`caw`可以达到同样的效果。所以`caw`更强大一些。

# 全选编辑
`ggvG` `ggVG`:全选, `gg`：是让光标移到首行，在vim才有效，vi中无效, `v`是进入Visual(可视）模式, `G`光标移到最后一行
 `ggyG` :全部复制
 `ggdG` : 全部删除
 
 # 保存
 命令模式：
 `:wq`退出保存
 `:q!`强制退出不保存

# 宏
- `q`：进入recording模式：
1.  Start recording by pressing q, followed by a lower case character to name the macro
2.  Perform any typical editing, actions inside Vim editor, which will be recorded
3.  Stop recording by pressing q
4.  Play the recorded macro by pressing @ followed by the macro name
5.  To repeat macros multiple times, press : NN @ macro name. NN is a number
参考：https://www.thegeekstuff.com/2009/01/vi-and-vim-macro-tutorial-how-to-record-and-play/
