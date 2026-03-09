Homework 4 – BlinkAgent Priority（FreeRTOS）
📌 專案介紹

本專案使用 FreeRTOS 在 Raspberry Pi Pico 上實作一個 Agent 架構的 LED 閃爍系統。

系統中每個 Agent 都會被建立成一個 FreeRTOS Task，由 RTOS 排程器負責執行。

本作業的主要目的是研究：

FreeRTOS 任務排程機制

Task Priority（任務優先權）

Agent-based 系統架構

嵌入式多工（Multitasking）

並且透過實驗觀察：

如果 BlinkAgent 設定為最高優先權（Highest Priority）會發生什麼事情？

⚙️ 系統架構

本專案採用 Agent-based architecture。

系統架構如下：

main.cpp
   │
   ├── Agent (基底類別)
   │
   └── BlinkAgent (繼承 Agent)
           │
           └── 控制 LED 閃爍
📂 專案目錄結構
homework-4-main
│
├── CMakeLists.txt
├── pico_sdk_import.cmake
├── FreeRTOS_Kernel_import.cmake
│
├── port/
│   └── FreeRTOS-Kernel/
│        ├── FreeRTOSConfig.h
│        ├── IdleMemory.c
│        └── cppMemory.cpp
│
├── src/
│   ├── main.cpp
│   ├── Agent.h
│   ├── Agent.cpp
│   ├── BlinkAgent.h
│   └── BlinkAgent.cpp
│
└── .vscode/
🔧 系統需求
硬體

Raspberry Pi Pico

軟體

需要安裝：

CMake

ARM GCC Toolchain

Raspberry Pi Pico SDK

FreeRTOS Kernel

建議開發環境：

Visual Studio Code

🚀 編譯方式
1️⃣ 下載專案
git clone <repository_url>
cd homework-4-main
2️⃣ 建立 build 資料夾
mkdir build
cd build
3️⃣ 執行 CMake
cmake ..
4️⃣ 編譯
make

完成後會產生：

xxx.uf2
5️⃣ 上傳到 Raspberry Pi Pico

按住 BOOTSEL

插入 USB

將 .uf2 檔案拖曳到 Pico

🧠 FreeRTOS 任務排程

在 FreeRTOS 中，每個 Agent 會被建立為一個 Task。

例如：

xTaskCreate(
    BlinkAgentTask,
    "BlinkAgent",
    stack_size,
    parameters,
    priority,
    NULL
);

RTOS 會根據 Priority（優先權） 決定哪個 Task 先執行。

⚡ BlinkAgent Priority 實驗

作業問題：

如果 BlinkAgent 設為最高優先權會發生什麼？

實驗結果

如果 BlinkAgent 是 最高 Priority

可能會發生：

BlinkAgent 頻繁執行

CPU 大部分時間都被 BlinkAgent 使用

其他 Agent 執行機會變少

這種情況稱為：

Priority Starvation（優先權飢餓）

低優先權任務可能會很少被執行。

📊 行為範例
正常 Priority
Agent A running
BlinkAgent running
Agent B running
BlinkAgent 最高 Priority
BlinkAgent running
BlinkAgent running
BlinkAgent running

其他 Agent 可能很少執行。

🎯 學習重點

透過本作業可以學習：

FreeRTOS Task 建立

Task Priority 排程

Agent-based 系統設計

嵌入式系統多工

Real-Time Operating System 概念
