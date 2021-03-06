# 第一章 Vim 的模式与切换

## 什么是 Vim 的模式

初学者可以尝试读一下内容，看不懂就看初学者的建议吧！

---

初学者进入 Vim 之后一定会迷惑于这三件事：怎么退出、怎么编辑、怎么保存？

StackOverFlow 上关于 Vim 浏览量第一的问题就是，如何退出 Vim ？虽然 Vim 在主界面已经说明了如何退出，但初学者还是疑惑：为什么是这样的呢？

一般的编辑器，我们一进去就可以编辑了。我在编辑器里键入 `a` ，编辑器中就应该插入 `a` ，编辑器理应是这样的，但为什么是这样呢？这与我键入 `<Ctrl>s` 有何不同呢？事实上，并没有什么不同，对于编辑器来说，二者都是击键，编辑器实现了键入 `a` 则插入 `a` ，键入 `<Ctrl>s` 则保存。因此，即使二者反一下，对于编辑器来说也不会有差别，但对于使用者来说，二者却天差地别，实际上，编辑器往往会约定俗成，键入 `a` 则插入 `a` 。

事实上， Vim 也是这样，只不过 Vim 并没有遵循这些约定罢了，这就给初学者带来了困扰。不过无妨，问题是， Vim 为什么要这样做呢？这样做到底有什么好处呢？

首先，我们首先得明确一些内容。对于编辑器来说，我们的键入对应是一系列事件，有定义则有事件，没有定义则没有事件。我们把有事件定义的键入视作一个集合。我们定义，在 Vim 中，这样一个集合称为一个模式，通过特殊的键入，使得当前模式切换到其他模式下，我们称之为模式切换。

Vim 的初学者往往搞不清楚什么是 Vim 的模式，其实就是一个固定的“键入-事件”集合。从定义我们可以看出，一般编辑器的只有一套“模式”，Vim 有多套，而任何一个具备按键自定义能力的且具有一定可编程配置的编辑器，其实都可以实现 Vim 模式， Vim 模式的泛化本质上是多模式而已。

Vim 这样设置多模式和模式切换有什么意义呢？首先， Vim 将模式分为了几个基本模式，常用的有普通模式、插入模式、可视模式、和命令模式等，分别对应了阅读、编辑、选择和设置与批处理等操作（非严格的划分）。因此， Vim 划分模式，并使用模式切换来切换操作，使得相近的操作可以在同一模式下完成，不会互相干扰，这就是模式划分最大的好处。

我们已经知道模式划分的好处，但是，为什么是普通模式作为 Vim 初始模式呢？编辑器难道不是用来编辑的吗？

首先，编辑前最重要的位置是确认要编辑的位置。 Vim 的普通模式提供了光标快速移动而不会改变文本的能力， 不能光看到 Vim 因为历史原因采用了 `h` `j` `k` `l`，也要看到 Vim 的 `w` `e` `f` `b` 这些键的光标跳跃能力，和 `\` 的查找能力。在普通模式击键而不编辑文本本身就是优点，因为本身就不需要编辑文本。当然，相对于鼠标而言，键盘的滚动似乎还不够方便，但是，在光标定位方面， Vim 的普通模式可以做到非常自然而精确的。

当然，初始模式其实可以改成插入模式的，但我认为，将普通模式作为 Vim 的初始模式是好的，因为想要做好编辑，最重要的是做好读，通过读来反复确认要编辑的内容，而且，普通模式提供了非常好的编辑与移动之间的切换与平衡。而且，通过后续的深入你会明白，这个“普通”，应该是“通用”的意思。普通模式才是所有模式中的主模式。

为什么说普通模式才是所有模式中的主模式呢？因为所有模式都可以切换到普通模式上，普通模式的操作是其他模式操作衍生的基础。这一点如果是长期使用 Vim 的同学应该能感受到。

其次，分开插入和普通，这样我们就可以定义无前缀的组合键了。比如在一般的编辑器里，你不能定义“=”为格式化，因为这样的话，你就不能正常输入“=”了，但现在， Vim 区分二者，这就意味着你就可以在普通模式下这么做了，好处有两点：一，快捷键语义化；二、减少修饰键。修饰键我指的是 `<Ctrl>` 、`<Alt>` 、`<Meta>` 、`<Super>` 和 `<Shift>` 。这些修饰键最大的问题就是你常去按容易磨手腕，容易得手部的疾病。所以，为了健康，用 Vim 吧！（笑

### 给初学者的建议

* 模式不清楚了，不对了，就按 `<ESC>` ，回到普通模式，不放心的话多按几次大都能回到。
* 首先把模式切换记住了，建议以普通模式为中心开始记，常用的切换至少记一个最通用的，然后开始下一步。更多的建议在能够使用 Vim 完成日常编辑后再记忆。

## 模式切换

模式切换对于新手来说是第一道难关。记住它并不难，但熟练的切换，而且还能确定当前是什么模式，对于新手来说是需要费一些功夫的了。

实际上，所谓的模式切换，主要是要掌握普通模式与其他模式之间相互切换。这里，我们只需要记住，其他模式回到普通模式，只需要按 `<ESC>` 就可以回来了，至于普通模式切换到其他模式，只需要记住一些常用的按键：

| 模式     | 按键                   |
| -------- | ---------------------- |
| 插入模式 | `i` 、`a` 、`I` 、 `A` |
| 可视模式 | `v` 、 `V` 、 `<C-v>`  |
| 命令模式 | `:`                    |

这里有个更简单的版本：

| 模式     | 按键                       |
| -------- | -------------------------- |
| 插入模式 | `i` ，按照 insert 去记忆。 |
| 可视模式 | `v` ，按照 visual 去记忆。 |
| 命令模式 | `:`                        |

注意，我在这里建议你养成习惯，将你的操作都赋予一层意义，这样子不仅仅是出于助记的目的，而且也出于养成在快速打字时不去思考按键只思考操作的习惯。当你比较 Vim 和其他编辑器的快捷键比较时，你会发现，这种区分模式的快捷键大大方便了快捷键的记忆。
