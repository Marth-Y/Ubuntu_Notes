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

  std::vector<const FeatLine*> not_related_featlines;
  std::map<int,std::vector<const FeatLine*>> related_groups; ^g49HipzR

ClassifyByTopoRelationship ^KaeRuNkH

Lane_ff ^xAat7xmp

DropBad:遍历所有线，根据起点距离自车的距离，设定线长阈值，超过线长则采用 ^tn7mBcFN

%%
## Drawing
```compressed-json
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
```
%%