# 🖥️ ysyx-F6 单周期 RISC-V CPU (基于 Logisim)
## ✨ 核心特性

* **完整的数据通路**：支持 RV32I 基础指令集，包含纯手工连线的 PC、ALU、Register File、ImmGen 和 LSU 模块。
* **哈佛/冯·诺依曼混合架构**：支持指令和数据的精准内存映射，完美处理字/字节寻址对齐。
* **VGA 外设驱动**：实现了地址为 `0x20000000` 的 MMIO，CPU 可直接向显存写入像素数据。
* **配套工具链 (Custom Toolchain)**：提供专属 Python 脚本，支持将任意照片转化为 CPU 可读的十六进制数据，并进行“外科手术式”的内存镜像注入。

---
## 📂 仓库结构

```text
📦 ysyx-F6-Project
 ┣ 📂 Logisim实验/
    ┣ 📜 Logisim实操.md                #Logisim完成F6超详细攻略图纸      
    ┗ 📜 minirv.circ                   # CPU 核心电路文件 (.circ)
 ┣ 📂 softwareExample/                 # 项目展示截图和说明文档配图
    ┣ 📜 vga.hex                       # 一生一芯LOGO
    ┗ 📜 my_full_color_vga_hex         # 作者头像
 ┣ 📂 tools/                           # 自动化构建工具链 (如 Python 转换脚本)
    ┣ 📜 importImage.py                # 自动转化图片至256*256再转成hex文件
    ┗ 📜 requirements.md               # 小小的配置的环境
 ┗ 📜 README.md                        # 项目说明文档
```
---
## 🛠️ 进阶玩法：在 CPU 上跑你自己的照片！
本项目自带了一个强大的 Python 工具，可以将你任意尺寸的照片转换为 32 位全彩 (RGB888) 格式，并精准注入到 CPU 的 RAM 镜像中，替换原有图像。
### 🚀 使用步骤
- **1.环境准备：** 确保你安装了 Python 3，并进入 tools/ 目录安装依赖库（详情见requirements.md)
- **2.准备照片：** 将你想要显示的图片重命名为 my_photo.jpg，并放入 tools/ 文件夹中。
(注：工具会自动将图片进行智能居中裁剪，压缩至 256x256 分辨率并适配 CPU 寻址。)
- **3.执行一键构建：** 在 tools/ 目录下运行脚本（请确保你的原始 vga.hex 也在同一级目录下或修改脚本路径）
- **4.加载新镜像：** 脚本运行成功后，会生成一个新的 .hex 文件（如 my_full_color_vga.hex）。该文件导入到 Logisim 的 ROM 和 RAM 中。⚠️ 硬件要求：由于全彩图片数据量较大，请务必确保 Logisim 中 RAM 组件的 Address Bit Width 至少设置为 19 位，否则会导致内存溢出。
- **5.点火起飞：** 复位并运行，等待你的专属照片在像素阵列中一点点显现！
---
### 📷 项目截图
#### 📟一生一芯LOGO
<img width="1445" height="1280" alt="3326b3a026537c6e7edbd73fb6e10d4b" src="https://github.com/user-attachments/assets/716270a5-a2e5-446b-9c09-e32ff63aa84e" />

#### 😎作者头像
<img width="1504" height="1225" alt="image" src="https://github.com/user-attachments/assets/f8331319-eb05-4b05-ba4d-2195ea98391b" />

### 🤝 致谢
💕💕感谢「一生一芯」项目组提供的优秀开源框架与实验指导，让从零手搓一颗芯片成为可能。🤩

