---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Excalidraw Data

## Text Elements
将不同相机的线合并为一个vector ^7PXuz2TO

将线分为topo相关线集合、topo无关的线 ^bjSLiT76

里面也会简要用横向线线(未关联的线与已关联的线)的距离，判断线是否应该与关键点关联 ^h9gwLw7p

ClassifyByTopoRelationship ^KaeRuNkH

DropBad:遍历所有线，根据起点距离自车的距离，设定线长阈值，超过线长则采用 ^tn7mBcFN

MergeRebuildFeatlinesInterface(topo_points,input_featlines_put_in_one_cam,merged_featlines) ^NepaHHSx

1. ReadTopoIdsFromInputFeatlines ^gn6TNvRB

遍历所有单帧的线得到关联的topo点，将点从近到远排序，最多取三个：sorted_topo_ids ^6j0yq2XK

2. 将上述sorted_topo_ids映射为topo_id到线的map。作为关联topo点的线集合，每根线只会和一个TOPO点绑定 ^XDYDpI1A

3. 遍历观测的线，尝试软关联，计算观测线与上述与topo点关联线的距离，距离近则认为也是关联的线，加入到对应的goup ^dzMqLx38

遍历 sorted_topo_ids，优先将已经绑定了 topo_id 的线分到对应 group，每条线只分到一个 group。 ^xyPmuc0q

std::map<int,std::vector<const FeatLine*>>& related_groups ^YmegYLem

4. 剩下的线全部归为无关线 ^cLZVI4Ng

%%
## Drawing
```compressed-json
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
```
%%