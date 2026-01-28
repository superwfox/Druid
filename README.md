# Druid

Minecraft 1.21.1 数据包，用于修改原版树木结构与植被生成密度。

## 功能

- **树木结构优化**：降低橡树、白桦树、云杉树的默认高度
- **植被密度控制**：大幅减少森林、针叶林的树木生成数量
- **草地优化**：降低草丛和高草的生成密度
- **花朵稀疏**：减少平原花朵生成

## 项目结构

```
Druid/
├── pack.mcmeta                           # 数据包配置 (pack_format: 48)
└── data/minecraft/worldgen/
    ├── configured_feature/               # 树木结构定义
    │   ├── oak.json                      # 橡树 (高度 3-4)
    │   ├── fancy_oak.json                # 大橡树 (基础高度 2)
    │   ├── birch.json                    # 白桦树 (高度 4-5)
    │   └── spruce.json                   # 云杉树 (高度 4-6)
    └── placed_feature/                   # 放置规则
        ├── oak_checked.json              # 橡树放置 (count: 0)
        ├── birch_checked.json            # 白桦放置 (count: 0)
        ├── spruce_checked.json           # 云杉放置 (count: 0)
        ├── trees_birch_and_oak.json      # 森林混合树 (90%不生成)
        ├── trees_taiga.json              # 针叶林树 (90%不生成)
        ├── patch_grass_plain.json        # 平原草地
        ├── patch_tall_grass.json         # 高草 (rarity: 8)
        └── flower_plain.json             # 平原花朵 (rarity: 16)
```

## 使用方法

1. 将 `Druid` 文件夹复制到存档的 `datapacks` 目录
   ```
   .minecraft/saves/<存档名>/datapacks/Druid
   ```

2. 进入游戏后执行 `/datapack enable "file/Druid"`

3. **重要**：世界生成修改仅影响新生成的区块，已生成区块不受影响

## 调整密度

修改 `placed_feature/*.json` 中的参数：

```json
// count: 0 = 不生成, 数字越大密度越高
{ "type": "minecraft:count", "count": 0 }

// rarity_filter: 数字越大越稀疏
{ "type": "minecraft:rarity_filter", "chance": 8 }

// weighted_list: 调整权重比例
"distribution": [
    { "weight": 9, "data": 0 },  // 90% 不生成
    { "weight": 1, "data": 1 }   // 10% 生成 1 棵
]
```
