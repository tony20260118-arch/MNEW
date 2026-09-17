graph LR
    %% Style Definitions
    classDef main fill:#f0f4f8,stroke:#102a43,stroke-width:2px;
    classDef pwr fill:#e0f2fe,stroke:#0284c7,stroke-width:2px;
    classDef ic fill:#fef9c3,stroke:#ca8a04,stroke-width:2px;
    classDef conn fill:#f0fdf4,stroke:#16a34a,stroke-width:2px;

    %% Main Input
    USB[USB Type-C<br>VBUS 5V / 3A / 15W]:::main

    %% DC-DC Regulators
    REG1["MT3124NQER (η=97%)<br>5V to 3.3V / 3.5A"]:::pwr
    REG2["MT3124NQER (η=90%)<br>5V to 0.9V / 3.5A"]:::pwr
    REG3["iD8212-ADA50R (η=75%)<br>5V to 1.8V / 1.2A"]:::pwr
    REG4["MT3124NQER (η=92%)<br>5V to 1.1V / 3.5A"]:::pwr
    REG5["MT3124NQER (η=97%)<br>5V to 3.3V"]:::pwr

    %% Main ICs & Connectors
    HUB["USB4 HUB<br>PS9010"]:::ic
    PD["PD3.1 IC<br>PS5513"]:::ic
    PCIE["USB4 to PCIe<br>ASM2464"]:::ic
    SD["USB3.2 to SD4.0<br>GL3232S"]:::ic
    CFEB["CFeB Connector"]:::conn
    SD4["SD4.0 Connector"]:::conn

    %% Connections & Rails
    USB -->|VBUS_5V<br>1.63A / 8150.74mW| REG1
    USB -->|VBUS_5V<br>560mA / 1848mW| REG2
    USB -->|VBUS_5V| REG3
    USB -->|VBUS_5V<br>656.63mA / 2166.9mW| REG4
    USB -->|VBUS_5V<br>1.36A / 6.8W| REG5

    %% Voltage Rail Routing
    REG1 -->|VCC33_SYS| HUB
    REG1 -->|VCC33_SYS| PD
    REG1 -->|VCC33_SYS| PCIE
    REG1 -->|VCC33_SYS| SD

    REG2 -->|0V9_PS9010| HUB

    REG3 -->|VCC18_2464| PCIE

    REG4 -->|VDD095_2464| PCIE

    REG5 -->|VCC33_CFe| CFEB

    %% Signaling & Enabler Paths
    REG5 -.->|HDD_PC_EN| PCIE
    SD -->|SD_V33<br>SD_V18| SD4
# MNEW