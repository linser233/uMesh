# 使用指南：在 uConsole 上安装并运行 uMesh 模块

English guide is here >>> [GUIDE_EN.md](https://github.com/linser233/uMesh/blob/main/GUIDE_EN.md)

## 硬件安装步骤

1. **关机 uConsole**  
   - 长按电源键彻底关机，并拔掉所有电源与外接线缆。  

2. **拆解 uConsole**  
   - 拆下后盖与固定螺丝，移除原有模块。  
   - 如果你购买的版本没有模块，则会看到 4G-LTE 模块的空板。  

3. **安装 uMesh 模块与挡板**  
   - 将 uMesh 模块对准接口与定位柱，平直插入并固定挡板。  
   - ⚠️⚠️⚠️ **注意：务必在未通电的情况下安装，否则可能导致 您的设备 模块永久损坏。**  

4. **安装后盖**  
   - 合上后盖并拧紧螺丝，确保外壳闭合良好。  

5. **安装天线**  
   - 将天线牢固拧紧在对应射频SMA接口。  
   - ⚠️⚠️⚠️ **警告：在任何情况下都不要在开机状态下未安装天线，否则将导致 uMesh 永久损坏。**  

---

## 软件配置步骤

6. **开机并安装 meshtasticd**  
   - 开机进入 Linux 系统，按照官方文档安装 meshtasticd：  
     [Meshtastic Linux 安装指南](https://meshtastic.org/docs/software/linux/installation)  

7. **获取并放置配置文件**  
   - 访问项目仓库 [meshtastic/firmware 官方GitHub](https://github.com/meshtastic/firmware/tree/develop/bin/config.d) 或 [uMesh GitHub](https://github.com/linser233/uMesh)  
   - 根据模块 PCB 或包装上的标记，下载 `lora-usb-umesh-1262.yaml` 或 `lora-usb-umesh-1268.yaml`。  
   - 将文件放入配置目录：  
     ```bash
     sudo cp lora-usb-umesh-126*.yaml /etc/meshtasticd/config.d/
     ```  
   - 💡 **提示：**这一步理论上是自动完成的，只有在需要手动调整发射功率或 `auto` 检测未能正常工作时才需要手动操作。  

8. **启动或重启 meshtasticd 服务**  
   - 使用 systemd 管理服务：  
     ```bash
     sudo systemctl enable meshtasticd
     sudo systemctl restart meshtasticd
     ```  

9. **开始使用**  
   - 验证节点信息：  
     ```bash
     meshtastic --info
     ```  
   - 如果能看到 `firmware_version`、`my_node_id` 等信息，说明配置成功。  
   - 🎉🎉🎉 Enjoy your Meshtastic network!  

---

## Tips & 注意事项

- **供电不足或计划外重启**  
  受限于uConsole的主板设计，如果出现意外重启或供电不足，请在 `lora-usb-umesh-126*.yaml` 中修改：  
  ```yaml
  SX126X_MAX_POWER: 22
  ```  
  💡 **提示：** 这个数值并不是真实的输出功率，具体请参考 [RF_Power.md](https://github.com/linser233/uMesh/blob/main/RF_Power.md)。  
  ⚠️ 此选项受到 **当地法律法规** 以及 **硬件能力** 的限制，请务必遵守。  


- **天线匹配**  
  使用与模块频段一致的天线（如 CN470、EU868、US915 等），避免损坏或性能下降。  