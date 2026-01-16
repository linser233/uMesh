# User Guide: Installing and Running the uMesh Module on uConsole

中文说明书在这里>>> [GUIDE_CN.md](https://github.com/linser233/uMesh/blob/main/GUIDE_CN.md)  

## Hardware Installation Steps

1. **Power off uConsole**  
   - Press and hold the power button to fully shut down, and disconnect all power and external cables.  

2. **Disassemble uConsole**  
   - Remove the back cover and screws, then detach the existing module.  
   - If you purchased a version without a module, you will see the 4G-LTE module placeholder board.  

3. **Install the uMesh module and bracket**  
   - Align the uMesh module with the connector and positioning posts, insert it straight, and secure the bracket.  
   - ⚠️⚠️⚠️ **Note: Always install with the device powered off, otherwise permanent damage to your device will occur.**  

4. **Reinstall the back cover**  
   - Close the back cover and tighten the screws, ensuring the enclosure is properly sealed.  

5. **Attach the antenna**  
   - Firmly screw the antenna onto the corresponding RF SMA connector.  
   - ⚠️⚠️⚠️ **Warning: Never power on the device without the antenna attached, otherwise permanent damage to uMesh will occur.**  

---

## Software Configuration Steps

6. **Power on and install meshtasticd**  
   - Boot into Linux and install meshtasticd following the official documentation:  
     [Meshtastic Linux Installation Guide](https://meshtastic.org/docs/software/linux/installation)  

7. **Obtain and place the configuration file**  
   - Visit the repositories [uMesh GitHub](https://github.com/linser233/uMesh).  
   - Based on the PCB or packaging label of your module, download the corresponding configuration file:  
     - `lora-usb-umesh-1262-30dbm.yaml`  
     - `lora-usb-umesh-1262-33dbm.yaml`  
     - `lora-usb-umesh-1268-30dbm.yaml`  
     - `lora-usb-umesh-1268-33dbm.yaml`
   - Place the file into the configuration directory:  
     ```bash
     sudo cp lora-usb-umesh-126*-**dbm.yaml /etc/meshtasticd/config.d/
     ```  
   - 💡 **Tip:** This step is usually handled automatically. Manual action is only required if you need to adjust transmit power or if `auto` detection does not work properly.  

8. **Start or restart the meshtasticd service**  
   - Manage the service with systemd:  
     ```bash
     sudo systemctl enable meshtasticd
     sudo systemctl restart meshtasticd
     ```  

9. **Begin using**  
   - Verify node information:  
     ```bash
     meshtastic --info
     ```  
   - If you can see `firmware_version`, `my_node_id`, and other details, the configuration is successful.  
   - 🎉🎉🎉 Enjoy your Meshtastic network!  

---

## Tips & Notes

- **Unexpected reboot or insufficient power**  
  Due to uConsole’s motherboard design, if unexpected reboots or power shortages occur, edit the `lora-usb-umesh-126*.yaml` file and set:  
  ```yaml
  SX126X_MAX_POWER: 22
  ```  
  💡 **Tip:** This value does not represent the actual RF output power. For detailed information, please refer to [RF_Power.md](https://github.com/linser233/uMesh/blob/main/RF_Power.md).  
  ⚠️ This option is subject to **local regulations** and **hardware limitations**. Please comply accordingly.  

- **Antenna matching**  

  Use an antenna that matches the module’s frequency band (e.g., CN470, EU868, US915) to avoid damage or degraded performance.  
