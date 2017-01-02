# 裝置描述

一個裝置被我們描述為一個 JSON 文件，除了基本硬體資訊（`hardware_info`，包含製造商、製造年份、等等資訊）之外，主要有：`uuid`（唯一識別碼）、
`type`（裝置類型，例如：電風扇、冷氣、燈具）、`traits` （裝置特點，例如：交流供電、WiFi 通訊、馬達）以及最重要的
`properties`（屬性，例如：馬達轉速、WiFi 網路參數、耗電量）。

這些是裝置的描述檔，當然當使用者註冊他的裝置後，必須告訴我們一個裝置置放的位置（`location`）、通訊地址（`address`）以及通訊方法
`proxy`（是否透過其他裝置）。

## 範例裝置描述檔

```json
{
	"hardware_info": {
		"manufacture": "Dyson",
		"manufactured": "2012-04-23T18:25:43.511Z"
	},
	"uuid": "bbbbc817-9fcc-42b2-b52d-d6851e38b1dd",
	"type": "fan",
	"traits": ["motorized", "plugged", "wifi_enabled"],
	"properties": [{
		"name": "standby",
		"data": "boolean",
		"type": "active",
		"text": {
			"property_name": "電源",
			"value_true": "待機中",
			"value_false": "使用中"
		}
	}, {
		"name": "speed",
		"data": "number",
		"type": "active",
		"metadata": {
			"min_value": 1,
			"max_value": 13
		},
		"text": {
			"property_name": "風速"
		}
	}, {
		"name": "consumption",
		"data": "number",
		"type": "passive",
		"text": {
			"property_name": "耗電量"
		}
	}]
}
```
每一部裝置，將會記錄自己的描述檔，並在配對時傳送給伺服器或是使用者的裝置。

## 伺服器端描述

```json
{
	"_id": "5349b4ddd2781d08c09890f3",
	"name": "電風扇",
	"location": "主臥房",
	"addresses": [{
		"type": "local-name",
		"address": "dyson-fan.local"
	}, {
		"type": "local-ip",
		"address": "192.168.1.130"
	}],
	"external_proxy": {
		"address": "4.4.12.30",
		"port": 1234
	},
	"device_info": {
		"hardware_info": {
			"manufacture": "Dyson",
			"manufactured": "2012-04-23T18:25:43.511Z"
		},
		"uuid": "bbbbc817-9fcc-42b2-b52d-d6851e38b1dd",
		"type": "fan",
		"traits": ["motorized", "plugged", "wifi_enabled"],
		"properties": [{
			"name": "standby",
			"data": "boolean",
			"type": "active",
			"text": {
				"property_name": "電源",
				"value_true": "待機中",
				"value_false": "使用中"
			}
		}, {
			"name": "speed",
			"data": "number",
			"type": "active",
			"metadata": {
				"min_value": 1,
				"max_value": 13
			},
			"text": {
				"property_name": "風速"
			}
		}, {
			"name": "consumption",
			"data": "number",
			"type": "passive",
			"text": {
				"property_name": "耗電量"
			}
		}]
	}
}
```
