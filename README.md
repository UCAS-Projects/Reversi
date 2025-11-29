# Reversi - 黑白棋MCTS算法实现

本项目是中国科学院大学（UCAS）2025年人工智能课程的第一次作业，实现了基于蒙特卡洛树搜索（MCTS）的黑白棋AI。

## 项目结构

```
Reversi/
├── 作业1-黑白棋+MCTS.ipynb          # 原始作业要求和框架
├── 黑白棋MCTS算法实现.ipynb         # 完整实现版本（推荐）
├── 算法实现报告.md                  # 详细的算法实现报告
├── README.md                        # 项目说明文档
└── LICENSE                          # 许可证
```

## 核心实现

### 1. UCB算法（任务一）

实现了Upper Confidence Bound算法用于MCTS的选择阶段：

$$UCB(v_i) = \frac{w_i}{n_i} + \sqrt{2} \times \sqrt{\frac{\ln N}{n_i}}$$

- **利用项**：选择胜率高的节点
- **探索项**：探索访问次数少的节点
- **理论保证**：渐进最优性

### 2. Roxanne启发式策略（任务二）

使用基于位置价值的启发式策略替代随机模拟：

- 角位（A1, H1, A8, H8）：最高优先级
- 中心稳定位置：次优先级
- X-square位置（B2, G7等）：最低优先级

### 3. 完整的MCTS框架

- **选择（Selection）**：UCB算法递归选择节点
- **扩展（Expansion）**：添加所有合法动作的子节点
- **模拟（Simulation）**：Roxanne策略快速模拟
- **反向传播（Backpropagation）**：更新统计信息

## 使用说明

### 环境要求

```bash
pip install func-timeout
```

### 运行AI对弈

打开 `黑白棋MCTS算法实现.ipynb`，运行所有cell后：

```python
# AI vs AI
black_player = AIPlayer("X", time_limit=2)
white_player = AIPlayer("O", time_limit=2)
game = Game(black_player, white_player)
game.run()
```

### 人机对弈

```python
# 人类 vs AI
black_player = HumanPlayer("X")
white_player = AIPlayer("O", time_limit=2)
game = Game(black_player, white_player)
game.run()
```

## 算法特点

- ✅ **理论完备**：UCB算法具有数学上的最优性保证
- ✅ **实践高效**：Roxanne策略显著提升模拟质量
- ✅ **代码规范**：详细注释，模块化设计
- ✅ **文档完善**：包含详细的算法实现报告

## 详细文档

查看 `算法实现报告.md` 获取：

- 详细的理论分析和公式推导
- UCB算法的数值示例
- Roxanne策略的领域知识解释
- 复杂度分析和优化方向
- 实验设计和结果讨论

## 性能参数

| 参数 | 推荐值 | 说明 |
|------|--------|------|
| time_limit | 2秒 | 每步思考时间 |
| 探索常数C | √2 | UCB算法探索常数 |
| 模拟次数 | ~400次/步 | 2秒内的平均模拟次数 |

## 技术栈

- Python 3.x
- 数学库：math（log, sqrt）
- 深度拷贝：copy.deepcopy
- 超时控制：func_timeout

## 作者

- **课程**：人工智能
- **学校**：中国科学院大学（UCAS）
- **日期**：2025年11月

## 参考文献

1. Browne et al. (2012). "A Survey of Monte Carlo Tree Search Methods"
2. Kocsis & Szepesvári (2006). "Bandit based Monte-Carlo Planning"
3. Canosa, R. "Analysis of Monte Carlo Techniques in Othello"

## License

详见 LICENSE 文件。
