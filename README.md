合作开发Unity2D横板游戏，个人负责部分：架构设计，enemy模块设计与实现等

# Enemy 模块（Unity）

本模块实现了一个 2D Unity 游戏的基础敌人系统。  
采用模块化架构，将 **运行时逻辑（Runtime）** 与 **展示逻辑（Presentation）** 分离。

## 文件夹结构

Assets/Script/

```
Bootstrap/
Enemy/
Player/
Shared/
```

### Enemy 模块

```
Enemy/
├── Presentation
│   ├── EnemyController.cs
│   └── EnemyAnimationController.cs
│
└── Runtime
    ├── AI
    ├── Combat
    ├── Data
    ├── Movement
    ├── Perception
    └── StateMachine
```

## 架构说明

敌人系统由多个子模块组成：

- **AI（人工智能）**  
  负责敌人的决策逻辑。

- **Perception（感知）**  
  使用传感器和 Layer Mask 检测玩家目标。

- **Movement（移动）**  
  控制 Rigidbody2D 的移动和面向方向。

- **Combat（战斗）**  
  管理攻击冷却、攻击范围和伤害逻辑。

- **StateMachine（状态机）**  
  控制敌人的状态，包括：
  - Idle（待机）
  - Patrol（巡逻）
  - Chase（追击）
  - Attack（攻击）
  - Return（返回）

## 主要类说明

### Enemy

核心运行时类，实现了以下接口：

- `IDamageable`（可受伤）
- `IAttacker`（攻击者）
- `IMovable`（可移动）
- `IFacing`（可面向）
- `ITargetable`（可被目标锁定）

负责协调：

- AI
- 状态机
- 战斗系统
- 移动系统
- 感知系统

### EnemyController

Unity 前端组件，功能包括：

- 初始化 Enemy 运行时系统
- 关联 Unity 组件（Transform、Rigidbody2D）
- 每帧更新 Enemy 逻辑

## 使用说明（调试/测试）

1. 在场景中创建一个 GameObject。
2. 添加组件：

```
Rigidbody2D
Collider2D
EnemyController
```

3. 创建一个 **EnemyConfig** 资源：

```
右键 → 创建 → Enemy → Enemy Config
```

4. 在 EnemyController Inspector 中关联该配置。
5. 设置 **Player layer** 并赋值给 PlayerMask。

## 注意事项

- 本模块重点在 **核心敌人逻辑**。
- 场景配置和玩法整合可由其他人或后续模块处理。
- 可添加 Gizmos 以调试感知范围和攻击范围。

## 作者

Enemy 模块为团队协作 Unity 项目的一部分实现。
