---
layout: post
title: 数字逻辑知识点总结
mathjax: true
---
## 第一章 开关变量

#### 1-1 数字系统（无知识点）

#### 1-2 数制与码制

- BCD码包括了有权码和无权码。
- 自然二进制码就是有权码和循环二进制码是无权码，也是可靠性编码。
- 8421码需要判9加6来进位。
- 2421码从5开始第一位为1，并且两边**互为反码**

-[ ] **2421码**和余3码产生进位的时候可以正确产生信号。

- 格雷码和BCD的双向转换相同：取第一个，第二个是第二个和第一个XOR。
- 奇偶校验码，第一位是校验位，区分奇、偶校验，编码所有位XOR可以得到校验位。

#### 1-3 逻辑函数以及其描述工具

- 真值表，逻辑代数式，逻辑图，卡诺图，波形图，硬件描述语言。
- 逻辑图中几种不同门的不同标准。
- 三态门：使能端无效时高阻态，可以组合做数据总线。

#### 1-4 布尔代数

- 基本公式里面的0-1律、互补律和等幂律（等幂律**与、或运算都满足**）。
- 分配律**与、或运算**都满足
- 常用公式：还原律、**吸收率**、**冗余律**
- 代入规则、反演规则、对偶规则。后两条用的时候要把同或和异或对换。
- 化简代数式的方法：并项、消项、消因子、配项

#### 1-5 卡诺图

- 相邻项是循环码才可以化简

- 注意题目中有固定的化简范围，比如只能每列之内合并

- 最小项表达式对各个最小项按序编号，可以有：  $$F=m_0+m_1+m_3$$

- 注意卡诺图的相邻的边

- **或与式**可以按找它的**反函数**来编写

- 有无关项时当作1来处理才能得到最简的表达式

#### 1-6 数字集成电路（无知识点）

#### 2-3 组合逻辑电路的等价变换

- 通用门有与非门和或非门
- 用两种通用门实现not、or、and、nor、not and逻辑


## 第二章 组合逻辑电路

#### 2-1 组合逻辑分析

- 组合逻辑分析步骤
- 有时候可以从表达式直接得到，有的时候必须要用真值表才可以看出来

#### 2-4 数据选择器与分配器

- 数据选择器MUX可以用En来拓展芯片容量，比如用来二合一

- 数据选择器用地址端A，选择数据输入端D，在En有效时输出D

- A的个数和D的个数的关系
 $$
n(D)=2^{n(A)}
 $$
- 数据选择器应用的时候地址位和有意义的输入高低位对应，其实就是当对应地址端的输入进行选择的时候，搞清楚这个时候**另外的输入**需要输入什么


- 应用数据选择器时，对卡诺图的化简要按照地址端的限制，注意不一定是按行
- 数据选择器是多输入，一输出；数据分配器是一输入，多输出

#### 2-5-1 译码器

- 译码器很像分配器，地址端 to 多个输出选一 
- 译码器的使能端有 $$G_1和G_2$$ ，其中 $$\overline {G_{2A}} \wedge \overline{G_{2B}}=1$$ 的时候  $$G_2$$ 有效
- 译码器**提供片选**，就是利用使能端在不同的译码器芯片之间做出选择
- 写出给定译码器选择的十六进制地址范围
- 在出相关应用题目的时候，注意使用**最小项表达式**，一个输入端对应一个变量。由于输出是低有效，所以译码器对最小项表达式适配的很好，最后只需要加上一个与非门
- 用译码器可以作数据分配器，使能端作数据输入端D
- 译码器+数据选择器作等值比较器
- 七段译码显示器有测试输入端$$\overline{LT}，$$熄灭输入端$$\overline{BI},$$灭零输入端$$\overline{RBI},$$灭零输出端$$\overline{RBO}$$
- 七段译码级联灭零的时候整数部分的高位RBO连接低位RBI，小数部分低位RBO连接高位RBI

#### 2-5-2 编码器

- 8-3优先编码器74LS148大数字优先级高，**反码输出**，$$\overline{E_o}$$低有效输出表示无输入状态，$$\overline{G_s}$$低有效输出表示有效输入（按下去了）,$$\overline E_I$$低有效输入的时候正常工作
- 8-3优先编码器74LS148设计16:4优先编码器，用高位$$E_o$$级联低位的$$E_I$$，得到扩容效果
- 8-3优先编码器74LS148设计二-十进制优先编码器，把多出来的2个输入位接入$$E_I$$，并且注意看真值表有哪个位的输出要调整

#### 2-6-1 数值比较器

- 从最高位开始比较，如果高位比较完，低位就变成无关项。级联的时候低位输出接入高位的级联输入。
- 级联输出只有在所有位都相等的情况下才会参考级联输入。

#### 2-6-2 加法器

- 串行进位加法器逐级传递进位，结构简单速度慢。
- 超前进位加法器进位**同时发生**，注意看式子。
- 利用全加器把5421码转为2421码使用高低位接法。
- 被减数和减数取**补码**作加法，有进位输出则结果位正，反之为负。
- 利用加法器完成加法操作的时候可以利用低进位来取补码。
- 四位全加器为8421码作加法的时候记得判9加6。

#### 2-6-3 奇偶校验器

- 74LS280，偶数个1EVEN输出1，奇数个1ODD输出1。
- 作为**奇校验位发生器**时，补上$$\oplus1$$，使得**ODD输出0**；同理，作为**偶校验位发生器**时，使用ODD输出，此时为0。
- 奇校验检验电路接收校验位发生器的信号$$\oplus$$上接收到的码串，再用ODD输出来控制接收器。

#### 2-1-5 竞争冒险

- **0冒险**和**1冒险**就是出现了不该出现的0和1，其中前者在$$A+\overline A$$会出现，后者是$$A\cdot \overline A$$
- 判断式子在什么情况下会出现冒险，可能有陷阱题，比如说某种冒险出现的条件无法满足
- 简单的可以通过加冗余项的方法来消除冒险。




## 第三章 时序逻辑

#### 3-1 双稳态触发器

- RS触发器一般是低有效
- 空翻：在一个门控信号的作用下，触发器状态变化多于一次的现象。寄存器可以解决锁存器的空翻问题
- 注意有没有**负边沿CP**
- JK触发器00维持，11翻转
- T触发器是J=K，所以T=0维持，T=1翻转

#### 3-2 时序分析

- Moore型，仅与现态相关；Mealy型，还和X输入有关
- 分析时序电路作用步骤：写出输出方程、激励方程和状态方程，列真值表，**画MDS状态图**
- 分析电路时说明是格雷码，以及有无自启动能力
- 重复/不重复检测序列

#### 3-3 锁存器和寄存器

- 锁存器使用：输入有效数据的稳定滞后于锁存信号
- 寄存器使用：输入的有效数据的稳定先于打入脉冲
- 移位寄存器
  - 环形计数器：尾接头，如果只有一位跟别的不一样，不用译码；无自启动；
  - 扭环形计数器：反相尾接头，0000初始可以得到**格雷码循环**；模数2N是环形的两倍；也没有自启动
- 中规模8位双向移位寄存器
  - 清零、置数、**保持**异步
  - 可以用于串并行转换
  - 计算机中的乘除运算部件，左移右移实现

#### 3-4 中规模计数器

- “大同小异”：说的是同步清零和异步清零；似乎置数端都是同步的
- $$E_P，E_T$$使能端同时为1才是计数状态，低位进位接高位使能端，$$C_o$$在四个为1的时候异步变成1
- 两片四位二进制计数器模为$$2^8=256$$，数字范围是0~255
- 可逆计数器：能做加法计数和减法计数
- 顺序脉冲发生器（节拍发生器）：计数器+译码电路（并行）
  - 移存型：环形/扭环形计数器；环形可以不用译码器；扭环形没有竞争冒险
  - 计数型：中规模计数器，利用率高，有竞争冒险
- 会分析计数器/移存+MUX的**序列信号发生器**，串行

#### 3-5 时序逻辑设计

- 画MDS状态 》》给状态编码然后列转移表》》卡诺图化简》》
- 画电路
- 注意状态转移表内的**无关项**一定要写出来并且放在卡诺图里面化简
- MDS图里面的**初始状态**就是**没有任何输入/序列失败的**状态
- **基本**RS触发器，低有效，至少有一个是无效的1；**同步**RS触发器，高有效，**有使能端**，至少有一个是0




## 第四章 存储系统

- 在CPU内部由寄存器（D触发器）构成的特殊存储部件有三种
  - 寄存器堆：数据寄存
  - 寄存器队列：指令队列
  - 寄存器栈：减少函数调用时对内存的访问
- **内存/主存储器**：RAM可读可写，但容易丢失；ROM只读，不易失，存放固定的程序和数据
- **单/双译码方式**，用一个/两个译码器，二维/三维存
- $$K=2^{10},M=2^{20},G=2^{30},1byte=8bit$$
- 容量为8KB时，可以得到$$8KB=8K\times 8=2^{13}\times 8$$，**有13根地址线（译码的时候需要的），8根数据线（一个传输单位的宽）**
- ROM=与门阵列（地址译码器）+或门阵列（存储矩阵，每个位用最小项表达式）



## 第五章 VHDL 

#### 5-1 基本结构

- 除了引号以内的字符，不区分大小写

- not, and, or 没有优先级，要用括号来体现

- 开头的通用句，把所有的库都包了

  ```vhdl
  library IEEE;
  USE IEEE.STD_LOGIC_1164.ALL;%逻辑型和逻辑运算
  USE IEEE.STD_LOGIC_UNSIGNED.ALL;%整数和标准逻辑之间的重载算术，比较函数
  USE IEEE.STD_LOGIC_ARITH.ALL;%标准逻辑的算术运算函数
  ```

- 注意entity里port声明的最后一行没有分号

  ```VHDL
  port (a,b: in std_logic;
       	c:out std_logic);
  ```

- std_logic是9值逻辑，除了‘0’，’1‘，还有‘Z’高阻态等

- integer 必须要**规定范围**，否则无法综合成电路，并且**不能使用逻辑操作符**

  ​	`signal s: integer range 0 to 15;`

- architecture结构体 

  - 声明举例 `signal e,f: std_logic;%数据对象+标识符+数据类型`
  - 主体内是**并行**的语句

- **数据对象**

  - 常量 constant `constant num: integer :=6; %常量要标明初值 `，`constant data :bit :='0'%不管是哪种数据对象，它们的数据类型可以是整形也可以逻辑型`
  - 变量 variable：用于局部数据的存储，描述算法，**只能在process里声明**；用**“:=”**赋值，赋值后没有延迟，立刻变化 ；感觉除了有loop的情况，基本上用不着variable
  - 信号 signal：代表实际的连线，**在architecture中声明**；用**"<="**赋值，先改变驱动值，也就是等式右边，但是**不立刻更新赋值**，比如在一个进程内是**等到整个进程结束时**再同时更新的

- 逻辑操作符“or、and”等**只用于bit，std_logic**类型，并且操作数的**宽度必须相等**

- 关系操作符（比较）：＝、/＝用于任何数据类型，其他用于整数、枚举类型、逻辑矢量

- 算数操作符

  - 除了&增加位宽以外，**四则运算都用于integer**；`temp<=('0'&a)+b`，只要有一个并置，整个右值就会加宽
  - 关于操作符的重载问题，在上机的时候integer+std_logic_vecter的操作会编译失败，所以这里重载的理解应该是原本只用于integer的'+'可以用于std_logic_vector+std_logic_vector

- 课件中出现的实现

  -[ ] 与非门
  -[ ] 38译码器
  -[ ] 四位二进制全加器（五位输出）

#### 5-2 行为描述

- **并行语句**和硬件的特点相匹配，**顺序语句**描述逻辑关系和算法

- 并行行为

  - 赋值语句（简单，选择，条件）：必须要 **位宽相同，数据类型相同**
  - 进程语句（process）
  - 例化语句（component）

- 并行赋值，作为组合逻辑，必须有"others","else"来覆盖所有情况，否则就会变成锁存器

  - 选择赋值：一个信号的不同值，无优先级，互斥

    ``` vhdl
    with scase select
      f<= d0 when "00",
       <= d1 when "01",
       <= d2 when "10",
       <= d3 when others;
    ```

  - 条件赋值：有优先级，而且不局限于单个信号，且不必互斥

    ```vhdl
    A<="000" when d(7)='0'else
       "001" when d(6)='0'else
       "010" when d(5)='0'else
       "111";
    ```

- 转向控制语句（**只在process中的顺序语句**)

  - if

    ```vhdl
    if (clk'event and clk='1') then %时钟上升沿
    	q0<=q1;
    	q1<=q2;
    	q2<=not q0; %利用signal的延迟更新，可以这样写扭环形计数器
    end if;
    ```

  - case

    ```vhdl
    CASE CS IS
      WHEN "00"=> z<=d0;
      WHEN "01"=> z<=d1;
      WHEN others=> z<=d2;
    ```

  - loop

    ```vhdl
    FOR i IN 0 TO 10 LOOP %这里的i是循环内部自动声明的
      temp:= temp+1; %如果这里不用variable，用signal，是无法实现的，因为只会更新一次
    END LOOP;
    ```

- 实现

  -[ ] 选择赋值实现四选一
  -[ ] 8-3优先编码器（条件赋值）
  -[ ] 3-8译码器（选择赋值）
  -[ ] 奇偶校验器

#### 5-3 描述风格

- process中，所有用到的输入信号都要出现的敏感信号列表

- 真值表必须完整反应（others，else）

- 同步/异步的复位/置位操作的实现

- 声明中的信号如`signal s1_temp: std_logic_vector(3 downto 0);`，默认初始值是“0000”吗？？？

- 对于输出如果没有中间变量会怎么样？

- 状态机，先把MDS图画出来，再对照着写代码就好

   - 利用在声明中的枚举类型实现，等于规定了新的数据类型： `type state is(s0,s1,s2,s3);\n signal current_state,next_state: state;`

   - 时序部分写状态方程；逻辑组合部分写输入和次态的关系（激励方程）

   - 利用case语句写的状态方程，利用两个signal来记录现态和次态

      ```vhdl
      CASE current_state IS
        when s0 => y<='0';
      	if x='0' then
            next_state<=s0;
      	end if;
        when s1 => y<='1';
      	if x='1' then
            next_state<=s0;
      	end if;
      END CASE;%这里没写others，因为已经都覆盖了
      ```

- component的使用

   - 元件声明：在同一个工程下写另一个entity，在main的architecture声明里面调用

      ```vhdl
      COMPONENT h_adder      
        PORT (  a，b :  IN STD_LOGIC;              
              co，so :  OUT STD_LOGIC);    
      END COMPONENT ； 
      ```

   - 元件例化：调用元件的过程，在architecture begin之后，u1是元件名

      ```vhdl
      u1: h_adder PORT MAP(ain,bin,d,e);%u1是元件名，并且端口顺序要对应
      u2: h_adder PORT MAP(a=>e,b=>cin,co=>f,so=>sum);%也可以通过指定端口的方法
      ```

      ​

- 实现

   -[ ] 异步低有效置数十进制计数器
   -[ ] 六十进制计数器
   -[ ] 八位环形移位寄存器（有用&的骚操作）
   -[ ] mealy型状态机
   -[ ] 四进制格雷码计数器