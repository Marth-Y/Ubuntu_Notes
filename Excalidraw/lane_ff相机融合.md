---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
将不同相机的线合并为一个vector ^7PXuz2TO

将线分为topo相关线集合、topo无关的线 ^bjSLiT76

里面也会简要用横向线线(未关联的线与已关联的线)的距离，判断线是否应该与关键点关联 ^h9gwLw7p

  std::vector<const FeatLine*> not_related_featlines;
  std::map<int,std::vector<const FeatLine*>> related_groups; ^g49HipzR

ClassifyByTopoRelationship ^KaeRuNkH

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.14",
	"elements": [
		{
			"type": "rectangle",
			"version": 230,
			"versionNonce": 419996854,
			"isDeleted": false,
			"id": "K8NmJHbshhGaj6TCbnsML",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -274,
			"y": -99.2421875,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 333,
			"height": 65,
			"seed": 305649066,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "NUbmQ4zdgiiuWTYXTYzkb",
					"type": "arrow"
				}
			],
			"updated": 1745904003465,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 52,
			"versionNonce": 906433194,
			"isDeleted": false,
			"id": "7PXuz2TO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -255,
			"y": -77.2421875,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 294.462890625,
			"height": 23,
			"seed": 162608618,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1745903386957,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "将不同相机的线合并为一个vector",
			"rawText": "将不同相机的线合并为一个vector",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "将不同相机的线合并为一个vector",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 116,
			"versionNonce": 1213052714,
			"isDeleted": false,
			"id": "bjSLiT76",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -284,
			"y": 89.7578125,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 357.8515625,
			"height": 23,
			"seed": 106060522,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1745903427017,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "将线分为topo相关线集合、topo无关的线",
			"rawText": "将线分为topo相关线集合、topo无关的线",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "将线分为topo相关线集合、topo无关的线",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 135,
			"versionNonce": 1659072310,
			"isDeleted": false,
			"id": "N_9PQN2ha1kdBtLOTQZE6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -308,
			"y": 76.7578125,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 410,
			"height": 52,
			"seed": 940567210,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "NUbmQ4zdgiiuWTYXTYzkb",
					"type": "arrow"
				}
			],
			"updated": 1745904003465,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 245,
			"versionNonce": 1885368874,
			"isDeleted": false,
			"id": "h9gwLw7p",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 185.59869855101658,
			"y": -29.224930301815505,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 793.3203125,
			"height": 23,
			"seed": 658386166,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1745928260666,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "里面也会简要用横向线线(未关联的线与已关联的线)的距离，判断线是否应该与关键点关联",
			"rawText": "里面也会简要用横向线线(未关联的线与已关联的线)的距离，判断线是否应该与关键点关联",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "里面也会简要用横向线线(未关联的线与已关联的线)的距离，判断线是否应该与关键点关联",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 108,
			"versionNonce": 2024053994,
			"isDeleted": false,
			"id": "UzicQNq7FyjVTgXzdWnP-",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 168.69255246394312,
			"y": -41.353298611111086,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 823.3333333333334,
			"height": 53.333333333333314,
			"seed": 57428790,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1745928260666,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 71,
			"versionNonce": 816271670,
			"isDeleted": false,
			"id": "NUbmQ4zdgiiuWTYXTYzkb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -112.88888888888903,
			"y": -24.686631944444514,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 6.666666666666629,
			"height": 92.22222222222223,
			"seed": 2043171562,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1745904027074,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "K8NmJHbshhGaj6TCbnsML",
				"focus": 0.013910196185697521,
				"gap": 9.555555555555486
			},
			"endBinding": {
				"elementId": "N_9PQN2ha1kdBtLOTQZE6",
				"focus": -0.0923326797766264,
				"gap": 9.222222222222285
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-6.666666666666629,
					92.22222222222223
				]
			]
		},
		{
			"type": "line",
			"version": 83,
			"versionNonce": 1428125098,
			"isDeleted": false,
			"id": "tm609o_LdIE-TEOg41ENo",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 96,
			"y": 78.64670138888897,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 75.55555555555543,
			"height": 73.33333333333331,
			"seed": 2119964790,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1745904030543,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					75.55555555555543,
					-73.33333333333331
				]
			]
		},
		{
			"type": "text",
			"version": 71,
			"versionNonce": 344810522,
			"isDeleted": false,
			"id": "g49HipzR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 185.99999999999955,
			"y": 120.86892361111126,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 703.125,
			"height": 48,
			"seed": 1953238134,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1748959650479,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "  std::vector<const FeatLine*> not_related_featlines;\n  std::map<int,std::vector<const FeatLine*>> related_groups;",
			"rawText": "  std::vector<const FeatLine*> not_related_featlines;\n  std::map<int,std::vector<const FeatLine*>> related_groups;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "  std::vector<const FeatLine*> not_related_featlines;\n  std::map<int,std::vector<const FeatLine*>> related_groups;",
			"lineHeight": 1.2,
			"baseline": 43
		},
		{
			"type": "line",
			"version": 53,
			"versionNonce": 1806578166,
			"isDeleted": false,
			"id": "FWARtnax8e3QJri4UQAHs",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 100.44444444444412,
			"y": 108.64670138888908,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 106.66666666666663,
			"height": 20,
			"seed": 1702416746,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1745904053758,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					106.66666666666663,
					20
				]
			]
		},
		{
			"type": "text",
			"version": 78,
			"versionNonce": 1350435462,
			"isDeleted": false,
			"id": "KaeRuNkH",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1196.0501780986083,
			"y": 71.49878877177355,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 304.6875,
			"height": 24,
			"seed": 1675057514,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1748959650480,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "ClassifyByTopoRelationship",
			"rawText": "ClassifyByTopoRelationship",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ClassifyByTopoRelationship",
			"lineHeight": 1.2,
			"baseline": 19
		},
		{
			"type": "rectangle",
			"version": 83,
			"versionNonce": 1855973930,
			"isDeleted": false,
			"id": "pWP7g3sSEU8b-frbrGkbC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1176.1796070849919,
			"y": 59.57644616360369,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 349.72204983965065,
			"height": 49.01407516692075,
			"seed": 336294634,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1745928252049,
			"link": null,
			"locked": false
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 2,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 3,
		"currentItemFontSize": 20,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 397.412807901315,
		"scrollY": 562.0616319444443,
		"zoom": {
			"value": 1.1
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%