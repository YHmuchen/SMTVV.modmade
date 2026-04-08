## 步骤 0：你需要的程序

- 虚幻引擎 4.27，你可以在 [虚幻引擎下载启动器](https://store.epicgames.com/en-US/download) 获取。
    - 提示：你可以安装到任何文件夹，为 UE4Editor.exe 创建快捷方式，然后稍后删除启动器。
- [Blender](https://www.blender.org/download/)，我使用的是 [3.6 版本](https://download.blender.org/release/Blender3.6/blender-3.6.9-windows-x64.msi)。
- [FModel](https://github.com/4sval/FModel)。
- [UAssetGUI](https://github.com/atenfyr/UAssetGUI/releases)。
- 需要同时拥有真女神转生 V 本体游戏和真女神转生 V 复仇
- 需要一个配置好密钥的模拟器，无论是 Ryujinx 还是 Yuzu，来提取游戏文件。

---

## 步骤 1：定位游戏文件

### PC 

- Steam 版：
1. 在你的 `Steam 库 > 管理 > 浏览本地文件` 中右键点击游戏。
2. 游戏文件夹 SMT5V 会打开，保持打开状态，跳到步骤 2。

### 模拟器

- Ryujinx：
1. 添加包含 SMTV .NSP 的游戏文件夹。
2. 右键点击游戏 > 提取数据 > RomFS。
3. 选择文件夹，点击确定并等待。

- Yuzu：
1. 添加包含 SMTV .NSP 的游戏文件夹。
2. `右键点击游戏 > 导出 RomFS`。
3. **选择程序**，点击确定。
4. **完整**，点击确定。
5. 应该会将游戏提取到 `%APPDATA%/Yuzu/dump/010069c01ab82000/romfs`。

---

## 步骤 2：准备 SMTV 文件

- 你需要 SMTV 本体，因为模型交换 mod 在发布时没有骨架，它使用恶魔的原始骨架，你需要导出一个骨架。

1. 打开 `romfs/Project/Content/Paks/~mods` 并将你的 mod 粘贴到那里。

---

## 步骤 3：导出角色
- 需要做两次，一次用于 SMTV（VNX），一次用于 SMTVV（VPC）。

1. **解压 FModel**。
2. 打开 FModel。
3. 点击 `目录 > 选择器`。
4. 点击 **添加未检测到的游戏** 下方的箭头图标。
5. 在 **目录** 中，选择：
    - （VVPC）`Path/to/SteamLibrary/common/SMT5V`。
    - （VNX）`Path/to/SMTV/ExtractedRomFS`。
6. 点击 `+ 按钮`。
7. 在顶部区域将 **UE 版本** 更改为：
    - （VVPC）`GAME_UE4_27`。
    - （VNX）`GAME_UE4_23`。

---

## 步骤 4：导出 mod 模型

1. 打开 SMT V 配置文件
2. 在顶部栏点击 `设置`。
3. 在**纹理平台**中选择 `Nintendo Switch`。
4. 在侧边栏将网格格式更改为 PSK
5. 将 pak 加载方式更改为 ALL
6. 加载 PAK
7. 进入被替换角色文件夹：
    - 如果是**主角**，也就是 Nahobino 形态的主角，进入 `Game/Design/Character/Player/pla603_hero_union`。
8. 右键点击 `pla603_hero_union` 文件夹，然后：
    - 导出文件夹包原始数据 (.uasset)
    - 保存文件夹包纹理 (.png)。
    - 保存文件夹包模型。
9. 在顶部栏点击 `设置`。
10. 在侧边栏将网格格式更改为 glTF 2.0 (binary)
11. 右键点击 `pla603_hero_union` 文件夹，然后：
    - 保存文件夹包模型。
12. 输出将在 `FModel 文件夹/Output/Exports/Project`。
13. 进入那个输出路径并将 `Project` 改为 `ProjectMod`，否则稍后会被覆盖。

---

## 步骤 5：导出未编辑模型
- 这一步对于修改了 Nahobino 的 mod 至关重要，因为从基础 SMTV 开始骨架就有变化，如果你不确定你的角色骨架是否有变化，可以比较骨架或者直接做这一步，这没有害处。

1. 打开 SMT VV 配置文件
2. 在顶部栏点击 `设置`。
3. 在**纹理平台**中选择 `PC`。
4. 在侧边栏将网格格式更改为 PSK。
5. 将 pak 加载方式更改为 ALL
6. 加载 PAK
7. 进入未编辑角色文件夹：
    - 如果是**主角**，也就是 Nahobino 形态的主角，进入 `Game/Design/Character/Player/pla603_hero_union`。
8. 右键点击 `pla603_hero_union` 文件夹，然后：
    - 导出文件夹包原始数据 (.uasset)
    - 保存文件夹包纹理 (.png)。
    - 保存文件夹包模型。
9. 移植不需要 glTF，因为我们稍后不会使用这个网格。
10. 输出将在 `FModel 文件夹/Output/Exports/Project`。

---

## 步骤 6：在 Blender 中导入并合并文件
- 对于改装角色导出：

1. 点击**导入 PSK** 并导入**本体游戏改装**角色的网格。
2. 转到 `文件 > 导入 > glTF` 并导入**本体游戏改装**角色的网格。
    - 如果 glTF 骨骼颠倒了，忽略它，继续按步骤操作。
3. 点击导入的 **glTF** 的**骨架对象**[1] 然后按住 `CTRL` 点击导入的 **PSK** 的**骨架对象**[3]。

![cTG5PheIcc](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/57c7972c-a739-4daf-bcd7-8f0a444f24be)

4. 在 PSK 插件中点击 **合并 PSK 和 GLTF**[3]。
    - 为什么要这样做？：PSK 通常不保留平滑组，导致网格无法保存，所以你使用带有 PSK 骨架的 glTF 网格。
5. 点击 **导入 PSK**。
6. 导入未编辑模型。

## 步骤 6.1：在 Blender 中更换骨架

1. 点击**改装网格**[1] 骨架内部，按住 `CTRL`，点击 **VV 的未编辑模型**[2]，然后将鼠标悬停在视口上并按 `CTRL + P` 选择**骨架变形**[3]。

![YMxExbhJfs](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/29773612-7051-4b6a-bdf9-a4c8d1ee5d55)

2. 删除**改装网格**的旧骨架。
3. 在**新骨架**上选择**改装网格**[1]，转到**修改器**[2] 并移除**旧骨架的修改器**[3]。

![xUGKOPpMBP](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/b6b45375-ebdc-4857-b1f8-39b8e5bc06a5)

4. 选择骨架并进入姿势模式，选择一些骨骼，主要是脊柱和腿部，做一些移动看看是否一切正常，之后按 `CTRL + Z` 回到 T 姿势。

## 步骤 6.2：处理新增网格
- 你可能会注意到 nahobino 有 4 把新剑，加上旧的一对总共 6 把，你可能想保留它们！

1. 回到对象模式，选择 **VV 的未编辑网格**，进入**编辑模式**。
2. 通过点击视口的空白区域取消选择所有内容。
3. 将鼠标悬停在每把剑上，每把剑按 `L`，`右键点击视口 > 分离 > 选中部分`

![blender_DZlw7uhfw5](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/576d1e19-ab65-4369-b418-3e8dea0ff7ae)

4. 你会注意到骨架下出现了一个新对象，进入**对象模式**并删除 **VV 的未编辑主体** 的网格。
5. 这样你就剩下 2 个网格，剑和改装网格。

## 步骤 6.3：检查材质名称
- FModel 似乎没有保留所有材质名称，修复它！（这部分是事后做的，所以截图中没有额外的剑网格，想象它们在那里）

1. 回到对象模式并选择**改装网格**[1]，进入**编辑模式**[2] 转到**材质**[3]，看看是否有任何条目叫做 `material_n`。

![mX1klIg2HH](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/9a00580f-4c1a-41ab-a9aa-8ee909f9d63f)

2. 如果是的话，你需要修复它，转到 **ProjectMod 输出文件夹** 中改装角色的**网格文件夹**，并用 UAssetGui 打开 mesh.uasset（例如 SK_pla603.uasset）。
3. 在名称映射中检查带有"Material"的路径，与 Blender 材质中缺失的进行比较。
4. 如果不止一个并且你不知道材质覆盖哪个部分：
    - 保持在编辑模式**取消选择所有内容**[1]，选择**未命名材质**[2] 然后点击**选择**[3]，那个材质的部分现在**被选中**[4]。

![CvT8CUELE6](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/0f6c4a17-e6be-4f72-b167-93a4204eac7b)

5. 双击重命名材质。

---

## 步骤 6：从 Blender 导出

1. 进入**对象模式**并保存项目。
2. 选择**骨架对象**。
3. 确保它命名为 **Armature**。
4. 在 PSK 插件中点击**导出为 FBX**。

---

## 步骤 7：导入到虚幻引擎 4.27

1. 打开**虚幻引擎 4.27** 并创建一个名为 Project 的空白项目，名称可选。
2. 创建角色的**网格文件夹**结构。
    - 对于 **主角** 就是 `/Content/Design/Character/Player/pla603_hero_union/Mesh`。
3. 将你从 Blender 导出的 FBX 重命名为与角色的 uasset 名称匹配（例如 `SK_pla603.fbx`）。
4. 将其拖放到 UE4 的 **Mesh 文件夹** 中。

![导入](https://user-images.githubusercontent.com/31487005/192072688-e1816da9-6101-492f-89bd-234f34548df7.png)

5. 勾选这些导入设置：**Use T0 As Ref Pose**、**Import Normals and Tangents**。

![导入设置](https://user-images.githubusercontent.com/31487005/192072789-174f671d-0c3a-47f6-8665-6ede0f2dd4b5.png)

---

## 步骤 8：准备烹饪

1. 如果模型有自定义纹理，查看它们在 **ProjectMod 文件夹** 的什么位置。
2. 在 UE4 中重新创建纹理文件夹并将它们移动到那里。
3. 选择它们，`右键点击 > 资源操作 > 通过属性矩阵批量编辑...`。
4. 勾选 **Compress Without Alpha** 并在 **Mip Gen 设置** 中选择 `NoMipmaps`。
5. 转到 `文件 > 全部保存`。
6. 关闭窗口。
7. 创建**材质文件夹**。
8. 将 UE4 创建的材质移动到**材质文件夹**。

## 步骤 8.1：创建 PostAnimBP（仅适用于 Pla601 或 Pla603）

1. 在 **Mesh 文件夹** 中右键点击 `SK_pla603 > 创建 > 动画蓝图`。
2. 命名为 `Pla603_PostAnimBP`。
3. 创建**以下文件夹**：
    - `/Content/Blueprints/Character/Player/Pla603/`。
4. 将 `Pla603_PostAnimBP` 移动到 **Pla603 文件夹**。

5. 在 **Mesh 文件夹** 中双击 `SK_pla603`。
6. 在 `资源详情` 侧边栏中，向下滚动到**骨骼网格体**部分。
7. 在**后处理动画蓝图**下拉菜单中找到 `Pla603_PostAnimBP`。
8. 关闭 `SK_pla603` 窗口。

## 步骤 8.2：设置物理资源（修复相机卡入身体）
- 这是主角 Pla603 的数值，其他角色：[学习如何获取它们。](https://github.com/mugenrei/mugenrei.github.io/wiki/SMTVV-%E2%80%90-Making-the-character's-PhAT)
1. 在 **Mesh 文件夹** 将 `SK_pla603_PhysicsAsset` 重命名为 `SK_pla603_PhAT` 并双击打开它。
2. 在 `骨架树` 侧边栏中，选择任意骨骼，按 `CTRL + A` 全选然后取消选择 `b_pelvis` 骨骼。
3. 右键点击选中内容并选择 `删除`。
4. 选择 `b_pelvis` 骨骼，在右侧选项卡的详情中：
    - 在**碰撞**下将**碰撞响应**更改为 `Disabled`。
    - 在**物理**下将**物理类型**更改为 `Kinematic`。
    - 在**主体设置**下展开**基元**、**胶囊体**和 **0**：
        - 将中心的 X 设置为 `-10`
        - 将中心的 Y 设置为 `90`
        - 将**半径**设置为 `70`
        - 将**长度**设置为 `70`
5. 关闭 `SK_pla603_PhAT` 窗口。

9. 转到 `文件 > 为 Windows 烹饪内容`。

---

## 步骤 9：创建 Mod 文件夹

1. 创建 mod 的工作文件夹，在本例中是**示例文件夹**。
2. 在这个文件夹里面你：
    - 解压 `UnrealPak.exe` 和伴随它的 `BAT 文件`。
    - 为 pak 创建一个文件夹，在这个例子中是 **exahero 文件夹**。
3. 在 **exahero 文件夹** 内创建来自 UE4 的 mod 文件夹结构。
    - 不需要材质或 Blueprints 文件夹。
4. 将烹饪后的 Mesh 文件夹中的**网格**和**物理资源**文件移动到 mod 的 Mesh 文件夹，**纹理**也一样。
    - 应该在 `D:\Documents\Unreal Projects\ProjectName\Saved\Cooked\WindowsNoEditor\ProjectName\Content\Design\Character\Player\pla603_hero_union`
    - 不要移动骨架 uasset，否则会破坏游戏。

---

## 步骤 10：处理额外材质和纹理
- 这里更多是概述/基本介绍关于材质，因为我现在缺乏如何更好地解释材质编辑的想法（如果你想改进它，请遵循页面顶部的 GitHub wiki 链接并修改它，我会很感激）。
- 你（大概）不能只复制本体游戏的材质，你需要一个在 UE 4.27 中烹饪过的，所以你使用游戏中的一个。

- 检查本体 mod 是否有与香草角色不同名称的纹理。
- 与香草文件夹相比，检查本体 mod 是否有额外材质。

- 如果两种情况都不是：
    - 也许这是一个将主角 Nahobino 形状改成 Giga 超大主角的 mod，那么可能不需要修改材质：
    1. 你完成了，进入打包步骤

- 如果是第一种情况：
    - 假设你正在移植一个附加了某些东西或将 Nahobino 替换为另一个模型的 Nahobino mod，那也需要不同的材质。

    1. 转到 **vv 角色材质** 文件夹。
    2. 复制一个你认为适合上一个材质位置的 **vv 材质**（例如，如果是皮肤，选择皮肤、hada、身体或脸部材质）到等效的**移植 mod 材质**文件夹。
    - 你需要在外部和文件内部重命名它，并调整路径，操作如下：
        1. 将名称从原始名称改为**本体游戏mod**的名称。
        2. 使用 **UAssetGui** 打开它。
        3. 在 **名称映射** 中，找到带有 **vv 材质** 名称的路径。
        4. 点击条目，复制，右键选择 `替换所有引用...`；注意：不要不这样做就直接更改。
        5. 粘贴路径并在路径末尾更改材质名称，路径应该从 `/Game/` 开始匹配材质当前所在位置。
        6. 仍然在 **名称映射**，向下滚动找到不带路径的 **vv 材质** 名称。
        7. 点击条目，右键点击它并选择 `替换所有引用...`，也更改它。
        8. 对纹理做同样的操作，将路径和独立条目重命名为**本体游戏mod**的名称。
        9. 保存并关闭。
---

## 步骤 11：打包并安装 Mod

1. 将 mod 的 **exahero 文件夹** 拖到 **unrealpak 的批处理文件** 上。

![打包 mod](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/65845995-bd6b-4b51-831a-de9bb3581fa5)

2. 将 `mod.pak` 复制到游戏的 **~mods 文件夹**。
    - 如果你没有安装 mod 的经验，请参考我的 Mod 安装指南。
3. **启动游戏**。

---

## 打开游戏
    - 你应该会注意到你所做的修改！

![SMT5V-Win64-Shipping_v6LT2Bq4y2](https://github.com/mugenrei/mugenrei.github.io/assets/31487005/c1f0d79d-f3c8-402c-8d5c-a261be87c9b5)

---

祝你改装愉快！
