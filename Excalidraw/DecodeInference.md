---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
struct LaneDecodeOutput
{
    uint32_t             frame_id;
    common::VehicleState vehicle_state;
    DetectedLanes        detected_lanes;
}; ^it0z9Zn2

DecodeInference(uint32_t frame_id,
                std::map<std::string, common::FeatureInfo_Void>& inference_features,
                common::VehicleState&                            vehicle_state,
                LanePitchEstimateOutputPtr                       pitch_for_decode,
                LaneRunonceOutputPtr                             hist_lane_result) ^mNv77XLB

return ^ZcVQoVb2

SetFeatureBuffer(inference_features) ^wPgRnY8A

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.14",
	"elements": [
		{
			"type": "text",
			"version": 408,
			"versionNonce": 1697508122,
			"isDeleted": false,
			"id": "it0z9Zn2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1270.8888888888896,
			"y": -734.4652777777783,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 468.75,
			"height": 144,
			"seed": 1746443078,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "JAulRYblTmkn2t_TbIMBk",
					"type": "arrow"
				}
			],
			"updated": 1748959846775,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "struct LaneDecodeOutput\n{\n    uint32_t             frame_id;\n    common::VehicleState vehicle_state;\n    DetectedLanes        detected_lanes;\n};",
			"rawText": "struct LaneDecodeOutput\n{\n    uint32_t             frame_id;\n    common::VehicleState vehicle_state;\n    DetectedLanes        detected_lanes;\n};",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "struct LaneDecodeOutput\n{\n    uint32_t             frame_id;\n    common::VehicleState vehicle_state;\n    DetectedLanes        detected_lanes;\n};",
			"lineHeight": 1.2,
			"baseline": 139
		},
		{
			"type": "text",
			"version": 578,
			"versionNonce": 598890118,
			"isDeleted": false,
			"id": "mNv77XLB",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -449.5555555555553,
			"y": -692.7986111111109,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 984.375,
			"height": 120,
			"seed": 220973830,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "JAulRYblTmkn2t_TbIMBk",
					"type": "arrow"
				}
			],
			"updated": 1748959854293,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "DecodeInference(uint32_t frame_id,\n                std::map<std::string, common::FeatureInfo_Void>& inference_features,\n                common::VehicleState&                            vehicle_state,\n                LanePitchEstimateOutputPtr                       pitch_for_decode,\n                LaneRunonceOutputPtr                             hist_lane_result)",
			"rawText": "DecodeInference(uint32_t frame_id,\n                std::map<std::string, common::FeatureInfo_Void>& inference_features,\n                common::VehicleState&                            vehicle_state,\n                LanePitchEstimateOutputPtr                       pitch_for_decode,\n                LaneRunonceOutputPtr                             hist_lane_result)",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "DecodeInference(uint32_t frame_id,\n                std::map<std::string, common::FeatureInfo_Void>& inference_features,\n                common::VehicleState&                            vehicle_state,\n                LanePitchEstimateOutputPtr                       pitch_for_decode,\n                LaneRunonceOutputPtr                             hist_lane_result)",
			"lineHeight": 1.2,
			"baseline": 115
		},
		{
			"type": "arrow",
			"version": 394,
			"versionNonce": 1804004614,
			"isDeleted": false,
			"id": "JAulRYblTmkn2t_TbIMBk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -470.6071551427592,
			"y": -661.6311868535265,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 324.444444444445,
			"height": 13.16408047115874,
			"seed": 1553047494,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "ZcVQoVb2"
				}
			],
			"updated": 1748959854293,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "mNv77XLB",
				"focus": 0.620188371065315,
				"gap": 21.051599587203896
			},
			"endBinding": {
				"elementId": "it0z9Zn2",
				"focus": 0.2919327363881001,
				"gap": 7.0872893016853595
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
					-324.444444444445,
					13.16408047115874
				]
			]
		},
		{
			"type": "text",
			"version": 7,
			"versionNonce": 2066420358,
			"isDeleted": false,
			"id": "ZcVQoVb2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -610.207849587204,
			"y": -664.5955521361809,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 70.3125,
			"height": 24,
			"seed": 534100698,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1748959850960,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "return",
			"rawText": "return",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "JAulRYblTmkn2t_TbIMBk",
			"originalText": "return",
			"lineHeight": 1.2,
			"baseline": 19
		},
		{
			"type": "text",
			"version": 81,
			"versionNonce": 2092369606,
			"isDeleted": false,
			"id": "wPgRnY8A",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -139.49604403164858,
			"y": -346.93603801169365,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 421.875,
			"height": 24,
			"seed": 478052314,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1748959869210,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 3,
			"text": "SetFeatureBuffer(inference_features)",
			"rawText": "SetFeatureBuffer(inference_features)",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "SetFeatureBuffer(inference_features)",
			"lineHeight": 1.2,
			"baseline": 19
		},
		{
			"text": "📍[[Mul_ToPo]]",
			"fontSize": 20,
			"fontFamily": 3,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 19,
			"id": "Y3qW8PJm",
			"type": "text",
			"x": -151.67108585858568,
			"y": -143.45715140123184,
			"width": 168.0859375,
			"height": 24,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"roundness": null,
			"seed": 65312,
			"version": 82,
			"versionNonce": 1907310214,
			"updated": 1748960141875,
			"isDeleted": true,
			"groupIds": [],
			"boundElements": [],
			"link": "[[Mul_ToPo]]",
			"locked": false,
			"containerId": null,
			"originalText": "📍[[Mul_ToPo]]",
			"rawText": "[[Mul_ToPo]]",
			"lineHeight": 1.2
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
		"scrollX": 870.2425144300141,
		"scrollY": 2205.77857997266,
		"zoom": {
			"value": 0.7000000000000002
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