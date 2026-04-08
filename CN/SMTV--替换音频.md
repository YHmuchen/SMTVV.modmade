## 工具
[AtomENCD, ACBEditor, PES Sound File (可选)](https://cdn.discordapp.com/attachments/878469784814096417/1137319474803003392/Tools.7z)

[unrealpak](https://cdn.discordapp.com/attachments/901222048288882749/1122762172171309146/unrealpak.7z)

[Unreal Model Viewer](https://www.gildor.org/en/projects/umodel#files)

AES 密钥: 0x5B23532568E0C4E82F4ABC7B22BCAC3599006FD106D9CD8AACD1BD4393FFDC61

[Foobar 的 vgmstream 组件 (可选)](https://github.com/vgmstream/vgmstream/releases)

## 指南
1. 使用 `umodel` 从 `Game\Sound\CueSheet\BGM` 提取 BGM 包到一个文件夹；
1. 然后将位于 `RomFS\Project\Content\Sound\Stream` 的 `BGM.awb` 复制到你提取包的同一个文件夹；
1. 现在你的文件夹内应该有 `BGM.uasset`、`BGM.uexp` 和 `BGM.awb`；
1. 使用 `HxD Editor` 打开 `BGM.uexp`，在文本部分搜索 `@UTF`，应该在文件开头附近；
1. 然后选中 `@UTF` 之前的所有内容并删除，现在你的文件应该以 `@UTF` 开头；
1. 转到 `文件 > 另存为…` 并保存为 `BGM.acb`；
1. 现在将 `BGM.acb` 拖放到 `ACBEditor.exe` 上；
1. 应该会创建一个包含 adx 文件的文件夹，这些就是音频文件；
    * 使用带有 `vgmstream` 组件的 `Foobar2000` 来打开 adx 文件并收听，否则如果你想通过这种方式收听，可以使用 `PES Sound` 将它们转换为 wav。
1. 现在你可以获取你电脑上的任何音乐，剪切、编辑然后保存为 wav；
1. 打开 `AtomENCD.exe`，加载文件然后更改设置，如果希望音乐循环就激活循环，`PES Sound` 也可以做同样的事情，除了自定义循环，默认情况下它会在音乐结束时循环，但如果你想要自定义循环：
    * 你可以使用 `Audacity` 获取循环时间点；
    * 打开 `Audacity`，加载 `.wav`，找到你认为可以循环的位置，然后选择整个循环区域；
    * 然后在时间线下方的栏上，在"选区"中，打开数字旁边的下拉菜单并将其更改为"样本"；
    * 在 `AtomENCD` 中将开关拨到"Custom Loop"；
    * 将选区上的数字写在"Start"和"End"上；
    * 关闭 `Audacity`。
1. 除了"Codec"之外，你可以在 `AtomENCD` 上更改任何你想要的设置*；
1. 现在将你的文件命名为与你要替换的文件相同的名称，然后进行替换*；
    >*在此之前请注意你要替换的音乐或语音文件与原文件的大小，我过去曾经遇到过问题（主要是语音文件，不记得音乐是否也有），使用比我要替换的文件更大的文件会出问题，如果你的文件更大，你可以在 AtomENCD 中更改设置来降低比特率（比如 44000 或 32000），除非你把比特率降得非常低，否则你不会注意到区别，或者你可以调整质量设置。
1. 现在将 BGM 文件夹拖到 `ACBEditor.exe` 上；
1. 现在用 HxD 打开 `BGM.acb` 和 `BGM.uexp`；
1. 在 `.acb` 文件中按 `Ctrl+A` 全选然后复制；
1. 在 `@UTF` 之前点击，然后按 `Ctrl+V`；
1. 现在向下滚动并选中所有未改变的字节直到末尾，除了最后 8 个字节 `C1 83 2A 9E`；
1. 右键并用零填充；
1. 保存 `.uexp`，应该会自动创建一个 bak 文件；
1. 现在在模拟器或 ftp 上创建 mod 文件夹结构；
1. 将 `BGM.awb` 传输到 `RomFS\Project\Content\Sound\Stream`；
1. 然后为 `BGM.uasset` 和 `BGM.uexp` 在任意位置创建 pak 目录，例如：`mod_name\Project\Content\Sound\CueSheet\BGM`；
1. 将 `mod_name` 文件夹拖入打包 bat；
1. 像安装任何其他 mod 一样安装。
