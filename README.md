# Hypervisor(virtual machine monitor): 又稱 虛擬機器監視器
虛擬機器管理程式 是我覺得比較好懂的解釋名詞
簡單說就是用來管理虛擬機器的程式，分為兩類
* 一類執行在硬體，這需要硬體有支援才行， 原生或裸機 hypervisor
  其中 Microsoft Hyper-V 是屬於 裸機 hypervisor
* 另一類則執行在作業系統上，就像其他電腦程式那樣執行，寄居或代管 hypervisor
  VirtualBox、VMware Workstation和VMware Workstation Player都是屬於這類
  
![hypervisor](https://user-images.githubusercontent.com/24542187/114294388-e02f3f80-9ad0-11eb-92d9-9c49688f91da.png)  
圖片來源:http://www.techplayon.com/what-is-hypervisor/

Hyper-V屬於BIOS級別，而不是在作業系統內執行的程式。因此即便沒有使用任何的虛擬機器
虛擬化服務也是處於開啟狀態，這樣可能會消耗掉一定的硬體資源

參考網站:https://www.mdeditor.tw/pl/pvLY/zh-tw

# hyper-v、WSL、WSL2
在windows虛擬出Linux環境的方式
1. 屬於Hypervisor type2
  * 子系統WSL
  * 安裝VMware等軟體  

  WSL架構圖  
  ![WSL-1-architecture](https://user-images.githubusercontent.com/24542187/114294581-4f596380-9ad2-11eb-8102-edcb8b13fbb5.png)  
  由此圖可以很明顯看到WSL是透過轉譯層，實際上並不包含Linux kernel

2. 屬於Hypervisor type1
  * Hyper-v
    Hyper-v架構圖:  
    ![070516_1410_WhatisHyper2](https://user-images.githubusercontent.com/24542187/114294764-4b7a1100-9ad3-11eb-9247-6c56ec8d97c2.png)  
    這張圖其實跟hypervisor type1並沒有什麼不同
    
  * WSL2  
    ![WSL-2-architecture](https://user-images.githubusercontent.com/24542187/114294880-13bf9900-9ad4-11eb-9af4-e9b2c1041f56.png)  
    由此圖可以看到WSL2才真的包含了Linux kernel
    
圖片來源:  
https://www.altaro.com/hyper-v/what-is-hyper-v/  
https://fossbytes.com/what-is-windows-subsystem-for-linux-wsl/

這裡是依照hypervisor的型別做分類，這裡有一篇wsl、wsl2架構比較
https://www.lijyyh.com/2020/07/linuxwindowswindows-subsystem-for.html

# Docker on windows
docker底層是用Linux kernel，要在windows上跑就必需額外啟用上述提到的虛擬技術  
較早的版本似乎是使用hyper-v虛擬技術(Windows Home版不支援啟動hyper-v)，
不過我安裝docker的時候已經是使用WSL2，也不需要hyper-v，據官方說法WSL2效能上要好很多

安裝WSL2:
啟動Virtual Machine Platform 與 Windows Subsystem for Linux  
![installWSL](https://user-images.githubusercontent.com/24542187/114295637-11ac0900-9ad9-11eb-85a2-d8c2af22ad3d.jpg)



都安裝好後可以下以下指令改成預設以WSL2啟動  
`wsl --set-default-version 2` 或 `wsl --set-version Ubuntu-18.04 2`  

安裝教學可參考:https://blog.walterlv.com/post/how-to-install-wsl2.html#%E7%AC%AC%E4%B8%89%E6%AD%A5%E5%90%AF%E7%94%A8-wsl2
* 官方下載的windows版docker基本上就是一直下一步，有缺少的就提醒要安裝
