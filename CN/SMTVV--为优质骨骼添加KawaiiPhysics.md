## 设置

- UE 4.27
- Kawaii Physics 插件，[这个版本](https://github.com/pafuhana1213/KawaiiPhysics/releases/tag/20221203-v1.10.0)。
- 需要具备模型和动画改装知识。

## 流程

1. 为你的模型创建一个动画蓝图。
![UE4Editor_wT6hgZwkoq](https://github.com/user-attachments/assets/ab20f323-7ba8-4ea8-bbb8-922c3569d23b)

2. 进入你的模型设置，找到骨骼网格体 > 后处理动画蓝图，将蓝图分配给它。
![UE4Editor_Iyv3o2PutC](https://github.com/user-attachments/assets/b1ef8272-7046-45d1-a26b-71ca2a988fcd)

3. 进入蓝图并添加一个输入姿势节点。
![QTCgQ2GBnD](https://github.com/user-attachments/assets/9a407cdc-2214-4ce7-819a-ca6f20b09def)

4. 然后添加一个 KawaiiPhysics 节点。
![2KJB6f6Df9](https://github.com/user-attachments/assets/88788d12-3876-43f6-930f-71be0cb3728e)

5. 连接所有节点，本地到组件节点会自动创建。
![UE4Editor_sWZYU5gsN5](https://github.com/user-attachments/assets/b24cc25b-2925-4ac2-9eef-3adbd99ab0aa)

6. 创建一个 Kawaii Physics 设置变量来存储物理设置。
![CBMGWX9md4](https://github.com/user-attachments/assets/f1f34207-55b4-428-bb8d-6f1f022a9705)

7. 点击编译，然后将 KawaiiPhysicsSettings 变量拖放到蓝图中。
![Wdvz6UQcMK](https://github.com/user-attachments/assets/89136038-b5ad-4526-9b80-fe1095953c67)

8. 选择 Kawaii Physics 节点，找到物理设置并将其暴露为引脚，然后将 KawaiiPhysicsSettings 节点连接到新引脚。
![UE4Editor_3SggNc77rr](https://github.com/user-attachments/assets/a0c417f5-9cf1-45e2-ad08-becf40d4840f)

9. 仍然在 Kawaii Physics 节点上，找到修改目标，在根骨骼中选择你要接收物理效果的骨骼，比如胸部骨骼！;)
    - 选择骨骼时，始终选择根骨骼，正如选项所说，那就是目标骨骼层级中的第一个骨骼。例如，如果你的角色胸部有 Boob00_L、Boob01_L、Boob03_L，你只需选择 Boob00_L，整个链就都会有物理效果。衣物同样适用！
![UE4Editor_sDXWzAYjnI](https://github.com/user-attachments/assets/6b495e9f-64c2-44db-b63c-71943d4b5687)

10. 如果你现在按编译，你可以通过转到动画观察物理效果生效！
![UE4Editor_NTvMH1jUr](https://github.com/user-attachments/assets/4e30905e-5107-4577-9359-2084aa5896b6)

12. 既然胸部是成对的，感谢上帝，你可以再添加一个 Kawaii Physics 节点并将它们链接起来！
![UE4Editor_LEIzUicvVV](https://github.com/user-attachments/assets/4e415b5e-8e0d-4e4b-848d-759688ec697a)

13. 然后选择另一根骨骼并将 Kawaii 设置连接到引脚。
![UsXRXG4ddK](https://github.com/user-attachments/assets/c4f7cf8f-8926-48a1-b698-29de25e6b740)

14. 然后你可以选择 Kawaii Physics 设置节点并调整数值，最重要的是阻尼（Damping）和刚度（Stiffness）。

15. 按编译，就完成了！

## 额外内容

- 你可以疯狂地将所有适用的骨骼添加到同一个蓝图中！
![UE4Editor_8K3ehffM4F](https://github.com/user-attachments/assets/7c8e310f-5bb9-4096-9062-5437262bc992)

- 你可以使用不同的设置创建不同的变量，例如一个用于胸部，另一个用于衣物，然后将它们分配给不同的节点。

- 你可以为每个节点创建碰撞胶囊体。
