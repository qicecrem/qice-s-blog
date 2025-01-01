### **8086 汇编指令概览**

#### **基本指令**
- **寄存器操作**
  - **查看寄存器内容**：`r` 命令。
  - **修改寄存器值**：如 `r ax` 后输入值。
   ```assembly
   r ax         ; 查看 AX 寄存器内容
   r ax, 1234H  ; 将 AX 寄存器的值修改为 1234H
   ```

- **内存操作**
  - **查看**：`d 段地址:偏移地址`。
  - **修改**：`e 段地址:偏移地址 数据...`。
  - **反汇编**：`u 段地址:偏移地址`。
   ```assembly
   d 0A00:0100          ; 查看内存地址 0A00:0100 开始的内容
   e 0A00:0100 12 34 56 ; 修改 0A00:0100 处的内容为 12H, 34H, 56H
   u 0A00:0000          ; 将 0A00:0000 处的机器码翻译为汇编指令
   ```

- **执行与控制**
  - **单步执行**：`t`（从 `CS:IP` 指向的地址开始执行一条指令）。
  - **写入指令**：`a`（向内存写入汇编指令）。
   ```assembly
   a 0A00:0100
   MOV AX, 1234H        ; 输入一条汇编指令
   ```

---

#### **数据传输**
- **`MOV` 指令**
  - 用于将数据从源传输到目标：
   ```assembly
   MOV AX, 1234H    ; 将数据 1234H 送入 AX
   MOV BX, AX       ; 将 AX 的值复制到 BX
   MOV AL, [0A00H]  ; 将内存地址 0A00H 的数据送入 AL
   ```

#### **算术操作**
- **`ADD` / `SUB`**
  - 加法与减法操作：
   ```assembly
   ADD AX, BX  ; AX = AX + BX
   SUB AX, 1   ; AX = AX - 1
   ```

- **`MUL` / `DIV`**
  - **乘法**
    - 8 位：`AL * 寄存器/内存` → 结果存于 `AX`。
    - 16 位：`AX * 寄存器/内存` → 高位存 `DX`，低位存 `AX`。
   ```assembly
   MUL BX      ; AX = AX * BX (16位乘法)
   ```
  - **除法**
    - 8 位：被除数为 `AX`，商存于 `AL`，余数存于 `AH`。
    - 16 位：被除数为 `DX:AX`，商存于 `AX`，余数存于 `DX`。
   ```assembly
   DIV CX      ; AX = DX:AX / CX
   ```

---

#### **程序流控制**
- **条件跳转**
  - **格式**：`CMP 目的, 源` + `JXX`。
   ```assembly
   CMP AX, BX ; 比较 AX 和 BX
   JE EQUAL   ; 如果相等则跳转到 EQUAL 标签
   ```
   ```
   JGE 前>=后     Jump if  greater or equal
   JG 前>后       Jump if  greater
   JLE 前<=后     Jump if  less or equal
   JL 前<后       Jump if  less
   JNE 前不等于后  Jump if not equal
   JE 前等于后     Jump if equal
   ```

- **循环控制**
  - 使用 `CX` 计数：
   ```assembly
   MOV CX, 5
   LOOP_START:
       ; 循环体
       LOOP LOOP_START  ; CX 减 1，若 CX ≠ 0 则跳转到 LOOP_START
   ```

---

#### **伪指令**
- **数据定义**
  ```assembly
  DATA SEGMENT
      ARR DB 1, 2, 3, 4  ; 定义字节型数组
      X   DW 1234H       ; 定义字型变量
      Y   DD 12345678H   ; 定义双字型变量
  DATA ENDS
  ```

- **段定义**
  - **代码段**：
   ```assembly
   CODE SEGMENT
   ASSUME CS:CODE, DS:DATA
   START: MOV AX, DATA
          MOV DS, AX
          ; 其他代码
          MOV AX, 4C00H
          INT 21H        ; 程序结束
   CODE ENDS
   END START
   ```

- **符号定义**
  ```assembly
  MAX EQU 10     ; 定义符号 MAX = 10
  ```

---

#### **中断调用**
- **`INT 21H` 功能调用**
  - **功能号**存于 `AH`，参数存于其他寄存器。
  - **常用功能号**：
    - **键盘输入字符**：`AH = 01H` → 字符存入 `AL`。
    - **单字符显示**：`AH = 02H`，字符存于 `DL`。
    - **显示字符串**：`AH = 09H`，`DX` 指向以 `$` 结尾的字符串。
    - **程序退出**：`AH = 4CH`。
   ```assembly
   MOV AH, 09
   MOV DX, OFFSET MSG ; DX 指向消息
   INT 21H            ; 调用中断显示字符串
   ```

---

### **完整程序示例**
1. **显示字符串**
   ```assembly
   DATA SEGMENT
   MSG DB 'Hello, World!$', 0
   DATA ENDS

   CODE SEGMENT
   ASSUME CS:CODE, DS:DATA
   START: MOV AX, DATA
          MOV DS, AX
          MOV AH, 09
          MOV DX, OFFSET MSG
          INT 21H
          MOV AX, 4C00H
          INT 21H
   CODE ENDS
   END START
   ```

2. **计算两个数的和**
   ```assembly
   DATA SEGMENT
   NUM1 DW 1234H
   NUM2 DW 4321H
   SUM  DW ?
   DATA ENDS

   CODE SEGMENT
   ASSUME CS:CODE, DS:DATA
   START: MOV AX, DATA
          MOV DS, AX
          MOV AX, NUM1
          ADD AX, NUM2
          MOV SUM, AX
          MOV AX, 4C00H
          INT 21H
   CODE ENDS
   END START
   ```

---
