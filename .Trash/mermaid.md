graph TD
    %% ================= 定义样式 =================
    classDef taskTitle fill:#1565C0,stroke:#0D47A1,stroke-width:2px,color:white,font-weight:bold,font-size:16px;
    classDef modelBox fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#0D47A1,stroke-dasharray: 5 5;
    classDef resultBox fill:#C8E6C9,stroke:#388E3C,stroke-width:2px,color:#1B5E20,shape:hexagon;
    

    classDef t1Group fill:#EBF5FB,stroke:#AED6F1;
    classDef t2Group fill:#FEF9E7,stroke:#F7DC6F;
    classDef t3Group fill:#F4ECF7,stroke:#D7BDE2;
    classDef t4Group fill:#E8F8F5,stroke:#A3E4D7;
    
    %% ================= 主体流程 =================
    
    %% ----- Task 1 -----
    subgraph T1_Area [Task 1: 潜在粉丝投票数据的逆向重构]
        direction TB
        T1_Goal[Goal: 逆向推断不可见的粉丝投票 $F_{it}$]:::taskTitle
        
        T1_Model(<b>模型与方法:</b><br>1. 贝叶斯逆问题框架<br>2. 单纯形上的逻辑正态先验<br>3. 硬约束: 历史淘汰结果<br>4. MCMC采样算法):::modelBox
        
        T1_Result{{<b>主要结果:</b><br>成功生成34赛季符合历史的 $\hat{F}_{it}$<br>发现粉丝评分方差显著大于裁判方差}}:::resultBox
        
        T1_Goal --> T1_Model
        T1_Model --> T1_Result
    end
    class T1_Area t1Group
    
    %% ----- 数据流向下一阶段 -----
    T1_Result ==>|提供重构数据基础| T2_Goal
    T1_Result ==>|提供重构数据基础| T3_Goal


    %% ----- Task 2 & 3 并行分析 -----
    subgraph Analysis_Phase [核心分析阶段]
        direction LR
        
        %% ----- Task 2 -----
        subgraph T2_Area [Task 2: 聚合机制对比与生存动力学]
            direction TB
            T2_Goal[Goal: 量化不同聚合机制对生存的影响]:::taskTitle
            
            T2_Model(<b>模型与方法:</b><br>1. 对比模型: 离散排名制 vs. 连续百分比制<br>2. 生存概率逻辑回归<br>3. 边缘情况敏感性分析):::modelBox
            
            T2_Result{{<b>主要结果:</b><br>发现排名制的'压缩效应'<br>排名制结构性放大粉丝权重<br>百分比制保留技术分差}}:::resultBox
            
            T2_Goal --> T2_Model
            T2_Model --> T2_Result
        end
        class T2_Area t2Group
    
        %% ----- Task 3 -----
        subgraph T3_Area [Task 3: 因素分析、偏差检测与验证]
            direction TB
            T3_Goal[Goal: 识别非技术因素与评估干预]:::taskTitle
            
            T3_Model(<b>模型与方法:</b><br>1. 固定效应回归 (人口学变量)<br>2. '裁判拯救'的统计评估<br>3. 历史争议的反事实模拟):::modelBox
            
            T3_Result{{<b>主要结果:</b><br>确认年龄偏见与'舞伴效应'<br>'拯救权'是条件性技术安全网<br>模拟证实排名制是争议根源}}:::resultBox
            
            T3_Goal --> T3_Model
            T3_Model --> T3_Result
        end
        class T3_Area t3Group
    end
    
    %% ----- 洞察流向优化设计 -----
    T2_Result ==>|机制缺陷洞察| T4_Goal
    T3_Result ==>|偏差与验证洞察| T4_Go
