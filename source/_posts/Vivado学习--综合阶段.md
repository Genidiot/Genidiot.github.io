# Vivado学习-综合阶段
> 本节使用版本为 vivado 2018.3
> 本节介绍顺序按照《Vivado从此开始 进阶篇》

综合部分主要分为**综合设置（Synth Design）**和**综合属性**，在vivado的**Flow Navigator**界面找到**SYNTHESIS**右键点击**Synthesis Settings** 即可打开综合设置界面，界面如下
![](2022-08-18-11-22-24.png)
## 综合设置
+ tcl.pre
  综合前的tcl命令
+ tcl.post
  综合后的tcl命令
+ -flatten_hierarchy
<table>
<tr>
  <th colspan="2">-flatten_hierarchy</th>
</tr>
<tr>
  <td>full</td>
  <td >综合时将原始设计打平，只保留顶层设计层次，执行边界优化</td>
</tr>
<tr>
  <td>none</td>
  <td>综合时完全保留原始设计层次，不执行边界优化</td>    
</tr>
<tr>
  <td>rebuilt</td>
  <td>综合时将原始设计打平，执行边界优化，综合后将网表文件按照原始设计层次显示，故与原始设计层次相似</td>
</tr>
</table>

+ -control_set_opt_threshold 
  对于同步复位、同步置位和同步使能信号，Vivado会根据-control_set_opt_threshold的设置进行优化，其目的是减少控制集的个数。优化方法》》》》
+ -no_lc
  勾选-no_lc时，不允许出现LUT整合
+ -keep_equivalent_registers
  当-keep_equivalent_registers没有被勾选即等效寄存器被合并时，等效寄存器可以有效降低扇出。
+ -resource_sharing
  对算术运算实现资源共享，只对算术运算，即加法和乘法运算有效
+ -gated_clock_conversion
  用于管理门控时钟(Gated Clock)，它可以将门控时钟信号变为使能信号
+ -fanout_limit
  全局选项，用于设定信号所能承载的最大负载，即最高的扇出个数，默认值为10000。需注意该选项对设计中的控制信号，如置位、复位和使能信号无效。
+ -shreg_min_size & -no_srlextract
  -shreg_min_size用于管理移位寄存器是否映射为LUT，默认值为3。
  -no_srlextract用于组织工具将移位寄存器映射为LUT。
+ -fsm_extraction
  用于设置状态机的编码方式
  