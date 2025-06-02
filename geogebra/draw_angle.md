- [geogebra入门-画一个等于已知角](https://www.bilibili.com/video/BV15M4m197Da)


- 使用函数

```
Rotate(point,angle,center)
```

![](https://s2.loli.net/2025/06/01/PMryENsX62jlodc.png)

## Angle 函数使用方法

- 官方文档 : https://geogebra.github.io/docs/manual/en/commands/Angle/

`Angle` 函数用于计算三个点构成的角度（点2为顶点），或两条线段/直线的夹角。

### 语法
```geogebra
Angle(点1, 点2, 点3)  // 计算三点形成的角度
Angle(线段/直线1, 线段/直线2)  // 计算两条线段的夹角
```

### 参数说明
- **点1, 点2, 点3**：三个点（点2为顶点），返回 ∠点1-点2-点3 的角度（0°~180°）。
- **线段/直线1, 线段/直线2**：两条线段或直线，返回它们的夹角（0°~90°）。

### 示例
1. **三点角度**：
   ```geogebra
   A = (1, 1)
   B = (2, 2)  // 顶点
   C = (3, 1)
   angle = Angle(A, B, C)  // 返回 90°
   ```

2. **线段夹角**：
   ```geogebra
   s1 = Segment((0,0), (2,2))
   s2 = Segment((0,2), (2,0))
   angle = Angle(s1, s2)  // 返回 90°
   ```

### 注意事项
- 角度单位为度（°）。
- 若输入无效（如重合点），返回 `undefined`。

![](https://s2.loli.net/2025/06/02/czuYh1JFP8TrKit.png)
