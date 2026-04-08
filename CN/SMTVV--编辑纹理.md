## 步骤 0：你需要的程序

- 虚幻引擎 4.27，你可以在 [虚幻引擎下载启动器](https://store.epicgames.com/en-US/download) 获取。
    - 提示：你可以安装到任何文件夹，为 UE4Editor.exe 创建快捷方式，然后稍后删除启动器。
- [UnrealPak](http://fluffyquack.com/tools/unrealpak.rar)
- [FModel](https://github.com/4sval/FModel)

---

## 步骤 1：在 UE 4.27 中创建项目

1. 打开虚幻引擎 4.27。
2. 创建一个新项目，选择空白，不包含启动资源。

---

## 步骤 2：导出纹理

1. **解压 FModel**。
2. 打开 FModel。
3. 点击 `目录 > 选择器`。
4. 点击 **添加未检测到的游戏** 下方的箭头图标。
5. 在 **目录** 中，选择：
    - `Path/to/SteamLibrary/common/SMT5V`。
6. 点击 `+ 按钮`。
7. 在顶部区域将 **UE 版本** 更改为：
    - `GAME_UE4_27`。

8. 记下游戏目录结构中纹理的原始路径。这对于重新导入至关重要。

---

## 步骤 3：编辑纹理

1. 在你喜欢的图像编辑软件中打开提取的纹理。
2. 对纹理进行必要的编辑。
3. 将编辑后的纹理保存为 PNG 或 TGA 格式，与原始文件同名。

---

## 步骤 4：将纹理导入虚幻引擎

1. 在 UE 4.27 中打开你的项目。
2. 导航到根目录中的 `Content` 文件夹。
3. 在 `Content` 文件夹中复制原始路径结构。
4. 将编辑后的纹理拖放到相应的文件夹中。

---

## 步骤 5：调整纹理设置

- **模型纹理**：纹理设置不需要更改。
- **UI 纹理**：
  1. 双击导入的纹理打开设置。
  2. 将 **压缩设置** 更改为 `VectorDisplacementmap`。
  3. 将 **Mip 生成设置** 设置为 `NoMipmaps`。
  4. 将 **纹理组** 设置为 `UI`。
  5. 保存。

---

## 步骤 6：烹饪项目

1. 导航到 `文件` 菜单。
2. 选择 `为 Windows 烹饪内容`。
3. 等待烹饪过程完成。
4. 输出应该在 `D:\Documents\Unreal Projects\ProjectName\Saved\Cooked\WindowsNoEditor\ProjectName\Content\...`

---

## 步骤 7：准备 Mod 文件夹

1. 为你的 mod 创建一个文件夹。
2. 在这个文件夹内，复制项目路径：`modfolder/Project/Content/...`。（注意：这次必须是 `Project`，而不是你给 UE4 项目起的名字。）
3. 将烹饪后的文件复制到这个路径中。

---

## 步骤 8：打包 Mod

1. 将 `modfolder` 拖放到 `UnrealPak-With-Compression.bat` 文件上。
2. 这将为你的 mod 创建一个 `.pak` 文件。

---

## 步骤 9：安装 Mod

1. 将 `.pak` 文件放入游戏的 `~mods` 文件夹。
2. 启动游戏，在游戏中查看你的修改。

---

恭喜！玩得开心！
