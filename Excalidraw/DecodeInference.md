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

{ ^pgFLmVLZ

%%***>>>text element-link:[[Mul_ToPo]]<<<***%%TOPOProcess ^5N2i2GOK

} ^ksPbmuvY

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
			"version": 704,
			"versionNonce": 1620834268,
			"isDeleted": false,
			"id": "mNv77XLB",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -441.4924823288967,
			"y": -892.9182232626295,
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
			"updated": 1749048190067,
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
			"version": 660,
			"versionNonce": 409776348,
			"isDeleted": false,
			"id": "JAulRYblTmkn2t_TbIMBk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -452.22960887447255,
			"y": -818.8776375161273,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 342.8219907127317,
			"height": 120.53110175996721,
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
			"updated": 1749048190068,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "mNv77XLB",
				"focus": 0.6978454705971847,
				"gap": 10.737126545575848
			},
			"endBinding": {
				"elementId": "it0z9Zn2",
				"focus": 0.3174378800603648,
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
					-342.8219907127317,
					120.53110175996721
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
			"version": 522,
			"versionNonce": 567948636,
			"isDeleted": false,
			"id": "wPgRnY8A",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -380.12637636424427,
			"y": -683.4359048247388,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 421.875,
			"height": 24,
			"seed": 478052314,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1749048190068,
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
			"id": "pgFLmVLZ",
			"type": "text",
			"x": -437.4558646625386,
			"y": -744.2428609458315,
			"width": 11.71875,
			"height": 24,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1038986204,
			"version": 214,
			"versionNonce": 472066524,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1749048190068,
			"link": null,
			"locked": false,
			"text": "{",
			"rawText": "{",
			"fontSize": 20,
			"fontFamily": 3,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 19,
			"containerId": null,
			"originalText": "{",
			"lineHeight": 1.2
		},
		{
			"text": "TOPOProcess",
			"fontSize": 20,
			"fontFamily": 3,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 19,
			"id": "5N2i2GOK",
			"type": "text",
			"x": -377.86113153313204,
			"y": -644.5362882100936,
			"width": 128.90625,
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
			"seed": 95198,
			"version": 286,
			"versionNonce": 978947676,
			"updated": 1749048190068,
			"isDeleted": false,
			"groupIds": [],
			"boundElements": [],
			"link": "[[Mul_ToPo]]",
			"locked": false,
			"containerId": null,
			"originalText": "TOPOProcess",
			"rawText": "TOPOProcess",
			"lineHeight": 1.2
		},
		{
			"id": "ksPbmuvY",
			"type": "text",
			"x": -429.4334967412723,
			"y": -555.1441885159838,
			"width": 11.71875,
			"height": 24,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1114849892,
			"version": 147,
			"versionNonce": 2102354652,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1749048190068,
			"link": null,
			"locked": false,
			"text": "}",
			"rawText": "}",
			"fontSize": 20,
			"fontFamily": 3,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 19,
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2
		},
		{
			"id": "xryHokgdJWtjdKnAWndIo",
			"type": "rectangle",
			"x": -468.3992837874224,
			"y": -928.757323134955,
			"width": 1138.0301922596286,
			"height": 777.0236358026467,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 120557540,
			"version": 219,
			"versionNonce": 2073470812,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1749048190068,
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
		"scrollX": 1575.6561949331715,
		"scrollY": 1421.781498097885,
		"zoom": {
			"value": 0.7725603299050771
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