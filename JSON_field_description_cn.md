# JSON 字段说明文档：结构面标注格式

该 JSON 文件格式适用于结构面（trace 和 facet）的标注任务，支持三维点云坐标、二维图像标注点、结构特性描述，以及使用 base64 编码存储的二值掩膜图像数据（兼容 Labelme 风格）。

---

## 顶层结构

```json
{
  "version": "1.0",
  "type": "structural_surface_annotation",
  "metadata": { ... },
  "shapes": [ ... ]
}
```

| 字段名       | 类型     | 描述                                           |
|--------------|----------|------------------------------------------------|
| `version`    | string   | 数据格式版本号                                 |
| `type`       | string   | 数据类型标识，此处为 `"structural_surface_annotation"` |
| `metadata`   | object   | 图像、点云及采集信息                           |
| `shapes`     | array    | 每个结构面的标注数据数组                       |

---

## `metadata` 字段

```json
"metadata": {
  "imagePath": "rock_surface_001.jpg",
  "pointCloudPath": "rock_surface_001.pcd",
  "imageHeight": 1024,
  "imageWidth": 1280,
  "sensor": "DJI Camera",
  "annotator": "geologist_A",
  "date": "2025-05-18"
}
```

| 字段名             | 类型     | 描述                                |
|--------------------|----------|-------------------------------------|
| `imagePath`        | string   | 标注所用图像文件路径或文件名        |
| `pointCloudPath`   | string   | 三维点云数据文件路径                |
| `imageHeight`      | integer  | 图像高度（像素）                    |
| `imageWidth`       | integer  | 图像宽度（像素）                    |
| `sensor`           | string   | 使用的传感器类型（如 RGBD + LiDAR） |
| `annotator`        | string   | 标注人或责任人名称                  |
| `date`             | string   | 标注日期（格式：YYYY-MM-DD）       |

---

## `shapes` 数组元素（结构面对象）

```json
{
  "id": "surface_001",
  "label": "trace",
  "description": { ... },
  "pixels_2d": [[x1, y1], [x2, y2], ...],
  "points_3d": [[x, y, z], ...],
  "mask": { ... }
}
```

| 字段名         | 类型     | 描述                                                 |
|----------------|----------|------------------------------------------------------|
| `id`           | string   | 结构面唯一标识符                                     |
| `label`        | string   | 结构面类型，可为 `"trace"`（线状）或 `"facet"`（面状）|
| `description`  | object   | 对结构面几何与性质的文字描述                        |
| `pixels_2d`    | array    | 图像上的二维标注点坐标（单位：像素）                |
| `points_3d`    | array    | 三维点云坐标（单位：米），与 `points_2d` 对应       |
| `mask`         | object   | base64 编码的掩膜图像信息，详见下节                 |

---

## `description` 字段（结构面特性）

```json
"description": {
  "filling_degree": "high",
  "aperture": "closed",
  "roughness": "smooth",
  "comments": "well cemented, no weathering"
}
```

| 字段名           | 类型   | 示例值                     | 描述                     |
|------------------|--------|----------------------------|--------------------------|
| `filling_degree` | string | `"none"` / `"partial"` / `"high"` | 填充程度               |
| `aperture`       | string | `"closed"` / `"open"`            | 张开度                 |
| `roughness`      | string | `"smooth"` / `"irregular"`       | 表面粗糙度             |
| `comments`       | string | 任意备注文字                    | 附加地质描述            |

---

## `mask` 字段（base64 图像数据）

```json
"mask": {
  "maskFormat": "png",
  "maskEncoding": "base64",
  "maskData": "iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAYAAACM..." 
}
```

| 字段名         | 类型     | 描述                                                   |
|----------------|----------|--------------------------------------------------------|
| `maskFormat`   | string   | 掩膜图像的文件格式，通常为 `"png"`                     |
| `maskEncoding` | string   | 编码方式，统一使用 `"base64"`                          |
| `maskData`     | string   | base64 编码的图像数据（PNG 单通道掩膜）                |

> ⚠️ 注意：`maskData` 内容通常很长，需由程序生成和解析。

---

## label 类型说明

| label 值 | 含义               |
|----------|--------------------|
| `trace`  | 结构面以线状痕迹表示 |
| `facet`  | 结构面以完整面片表示 |

---

## 📎 用途说明

该数据格式适用于：
- 三维地质结构面建模
- 裂隙识别与性状分类任务
- 图像与点云联合分割训练
- 学术研究中的结构面定量分析

---
If you have any question, please kindly email me.
