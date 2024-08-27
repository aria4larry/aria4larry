

### 混淆矩阵
| 实际图片是否正常 | GPT检测否 | GPT检测是 | 总计 |
| ---------------- | --------- | --------- | ---- |
| 否               | 451       | 1         | 452  |
| 是               | 8         | 230       | 238  |
| 总计             | 459       | 231       | 690  |

### 正样本指标
1. **准确率（Accuracy）**： 所有预测中正确预测的比例
2. **精确率（Precision）**： 预测为正样本中实际为正样本的比例
3. **召回率（Recall）**： 实际为正样本中被正确预测为正样本的比例 
4. **F1分数（F1 Score）**：精确率和召回率的调和平均数 
#### 计算公式
1. **准确率（Accuracy）**: 
   $$
   \text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
   $$

2. **精确率（Precision）**: 
   $$
   \text{Precision} = \frac{TP}{TP + FP}
   $$

3. **召回率（Recall）**: 
   $$
   \text{Recall} = \frac{TP}{TP + FN}
   $$

4. **F1分数（F1 Score）**: 
   $$
   \text{F1 Score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
   $$

#### 计算步骤
- **True Positive (TP)**: 实际是正常，检测为正常 = 230
- **True Negative (TN)**: 实际是不正常，检测为不正常 = 451
- **False Positive (FP)**: 实际是不正常，检测为正常 = 1
- **False Negative (FN)**: 实际是正常，检测为不正常 = 8

1. **准确率（Accuracy）**:
   $$
   \text{Accuracy} = \frac{230 + 451}{230 + 451 + 1 + 8} = \frac{681}{690} \approx 0.98696
   $$

2. **精确率（Precision）**:
   $$
   \text{Precision} = \frac{230}{230 + 1} = \frac{230}{231} \approx 0.99567
   $$

3. **召回率（Recall）**:
   $$
   \text{Recall} = \frac{230}{230 + 8} = \frac{230}{238} \approx 0.96639
   $$

4. **F1分数（F1 Score）**:
   $$
   \text{F1 Score} = \frac{2 \times 0.99567 \times 0.96639}{0.99567 + 0.96639} \approx 0.98081
   $$

#### 结果
- **准确率（Accuracy）**: 98.70%
- **精确率（Precision）**: 99.57%
- **召回率（Recall）**: 96.64%
- **F1分数（F1 Score）**: 98.08



### 负样本指标
1. **特异度（Specificity）**: 正确识别负样本的比例。
2. **假正率（False Positive Rate, FPR）** : 错误识别为正样本的负样本比例。
3. **假负率（False Negative Rate, FNR）**: 错误识别为负样本的正样本比例。
4. **负预测值（Negative Predictive Value, NPV）**: 预测为负样本中实际为负样本的比例。

#### 计算公式
1. **特异度（Specificity）**:
   $$
   \text{Specificity} = \frac{TN}{TN + FP}
   $$

2. **假正率（False Positive Rate, FPR）**:
   $$
   \text{FPR} = \frac{FP}{FP + TN}
   $$

3. **假负率（False Negative Rate, FNR）**:
   $$
   \text{FNR} = \frac{FN}{FN + TP}
   $$

4. **负预测值（Negative Predictive Value, NPV）**:
   $$
   \text{NPV} = \frac{TN}{TN + FN}
   $$

#### 计算步骤
- **True Negative (TN)**: 451
- **False Positive (FP)**: 1
- **False Negative (FN)**: 8
- **True Positive (TP)**: 230

1. **特异度（Specificity）**:
   $$
   \text{Specificity} = \frac{451}{451 + 1} = \frac{451}{452} \approx 0.99779
   $$

2. **假正率（False Positive Rate, FPR）**:
   $$
   \text{FPR} = \frac{1}{1 + 451} = \frac{1}{452} \approx 0.00221
   $$

3. **假负率（False Negative Rate, FNR）**:
   $$
   \text{FNR} = \frac{8}{8 + 230} = \frac{8}{238} \approx 0.03361
   $$

4. **负预测值（Negative Predictive Value, NPV）**:
   $$
   \text{NPV} = \frac{451}{451 + 8} = \frac{451}{459} \approx 0.98257
   $$

#### 结果
- **特异度（Specificity）**: 99.78%
- **假正率（False Positive Rate, FPR）**: 0.22%
- **假负率（False Negative Rate, FNR）**: 3.36%
- **负预测值（Negative Predictive Value, NPV）**: 98.26%


### 模型评估指标

#### 1. 正样本指标
正样本指标用于评估模型在识别正样本（即实际正常的图片）方面的表现。

| 指标                | 简要说明                               | 计算公式                                                                                                    | 结果   |
| ------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------ |
| 精确率（Precision） | 预测为正样本中实际为正样本的比例       | $\text{Precision} = \frac{TP}{TP + FP}$                                                                     | 99.57% |
| 召回率（Recall）    | 实际为正样本中被正确预测为正样本的比例 | $\text{Recall} = \frac{TP}{TP + FN}$                                                                        | 96.64% |
| F1分数（F1 Score）  | 精确率和召回率的调和平均数             | $\text{F1 Score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$ | 98.08% |

#### 2. 负样本指标
负样本指标用于评估模型在识别负样本（即实际不正常的图片）方面的表现。

| 指标                                       | 简要说明                               | 计算公式                                  | 结果   |
| ------------------------------------------ | -------------------------------------- | ----------------------------------------- | ------ |
| 特异度（Specificity）                      | 实际为负样本中被正确预测为负样本的比例 | $\text{Specificity} = \frac{TN}{TN + FP}$ | 99.78% |
| 假正率（False Positive Rate, FPR）         | 实际为负样本中被错误预测为正样本的比例 | $\text{FPR} = \frac{FP}{FP + TN}$         | 0.22%  |
| 假负率（False Negative Rate, FNR）         | 实际为正样本中被错误预测为负样本的比例 | $\text{FNR} = \frac{FN}{FN + TP}$         | 3.36%  |
| 负预测值（Negative Predictive Value, NPV） | 预测为负样本中实际为负样本的比例       | $\text{NPV} = \frac{TN}{TN + FN}$         | 98.26% |

#### 3. 整体情况指标
整体情况指标用于评估模型在整体上的表现。

| 指标               | 简要说明                 | 计算公式                                              | 结果   |
| ------------------ | ------------------------ | ----------------------------------------------------- | ------ |
| 准确率（Accuracy） | 所有预测中正确预测的比例 | $\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$ | 98.70% |

### 模型评价
- **正样本识别**: 模型在识别正样本（即实际正常的图片）方面表现非常好，精确率为99.57%，召回率为96.64%，F1分数为98.08%。这表明模型在预测为正样本时很少出错，并且能够识别出大多数的正样本。
- **负样本识别**: 模型在识别负样本（即实际不正常的图片）方面表现也非常好，特异度为99.78%，假正率为0.22%，假负率为3.36%，负预测值为98.26%。这表明模型在预测为负样本时非常准确，并且能够正确识别大多数的负样本。
- **整体表现**: 模型的整体准确率为98.70%，表明模型在所有预测中有很高的正确率。

总体而言，模型在识别正样本和负样本方面都表现出色，具有很高的精确率、召回率和特异度，适用于需要高准确率和低误判率的应用场景。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ3MDYzMDJdfQ==
-->