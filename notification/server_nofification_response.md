INBOX 通知類型 Server Response 說明
==

> 2016.11.16 特別說明
> 在下星期三恩平回來前, 
> 會先把 type = app_upgrade.new, extra key 改為 upgrade_data 
> 其餘 type 的 extra 則改為 ring_data
> 但在格式確認前會新舊並存

---

|Type|Description|Type|Description|
|----|----|----|----|
|out_of_fence|離開柵欄|sos|SOS通知(2)|
|low_battery.25|低電量通知(25%)|low_battery.5|低電量通知(5%)|
|firmware_upgrade.new|韌體更新通知|firmware_upgrade.success|韌體更新成功|
|firmware_upgrade.fail|韌體更新失敗|no_signal|無訊號通知(6hr)|
|app_upgrade.new|有APP更新項目|end_of_service|服務到期|
|ring_sharing|被分享手環資訊|ring_sharing.success|被分享手環同意|
|ring_sharing.fail|被分享手環不同意|

  
> 補充說明: type = ring_sharing, 目前未實作.

----

|Type|MESSAGE_TYPE
|----|----|
|out_of_fence|1|
|sos|2|
|low_battery.25|3|
|low_battery.5|4|
|firmware_upgrade.new|5|
|firmware_upgrade.success|6|
|firmware_upgrade.fail|7|
|no_signal|8|
|app_upgrade.new|9|
|end_of_service|10|
|ring_sharing|11|
|ring_sharing.success|12|
|ring_sharing.fail|13|

----

Inbox Server Response Sample:


    {
      "data": [
        {
          "id": 1,
          "type": "out_of_fence",
          "is_read": -1,
          "message": "{ring_name}在{time}離開柵欄",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "img_path": "string",
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z",
            "last_location": {
              "ring_sn": "ring_name",
              "type_code": "L2",
              "longitude": 25.12312312,
              "latitude": 102.123123123,
              "type": "gps",
              "battery_power": 100,
              "timestamp": "2016-10-12T15:30:15Z"
            },
            "fence_setting": [
              {
                "fence_name": "fence_name",
                "longitude": 25.12312312,
                "latitude": 102.123123123,
                "radius": 500,
                "report_rate": 30,
                "start_time": "18:00",
                "end_time": "19:00",
                "fence_no": 1
              }
            ],
            "timestamp": "2016-10-12T15:30:15Z"
          }
        },
        {
          "id": 2,
          "type": "sos",
          "is_read": -1,
          "messge": "{ring_name}發出SOS通知",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z",
            "last_location": {
              "ring_sn": "ring_sn",
              "type_code": "L2",
              "longitude": 26.12312,
              "latitude": 102.123123,
              "type": "gps",
              "battery_power": 100,
              "timestamp": "2016-10-15T15:30:15Z"
            },
            "timestamp": "2016-10-12T15:30:15Z"
          }
        },
        {
          "id": 3,
          "type": "low_battery.25",
          "is_read": 0,
          "messge": "{ring_name}電量低於25%",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z",
            "last_location": {
              "ring_sn": "ring_name",
              "type_code": "L0",
              "longitude": 25.123123,
              "latitude": 102.12312312,
              "type": "gps",
              "battery_power": 25,
              "timestamp": "2016-10-09T15:30:15Z"
            },
            "timestamp": "2016-10-12T15:30:15Z"
          }
        },
        {
          "id": 4,
          "type": "low_battery.5",
          "is_read": 0,
          "messge": "{ring_name}電量低於5%",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z",
            "last_location": {
              "ring_sn": "ring_name",
              "type_code": "L0",
              "longitude": 25.123123,
              "latitude": 102.12312312,
              "type": "gps",
              "battery_power": 5,
              "timestamp": "2016-10-09T15:30:15Z"
            },
            "timestamp": "2016-10-12T15:30:15Z"
          }
        },
        {
          "id": 5,
          "type": "firmware_upgrade.new",
          "is_read": 0,
          "messge": "{ring_name}有新版韌體更新",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 1,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z"
          },
          "timestamp": "2016-10-12T15:30:15Z"
        },
        {
          "id": 6,
          "type": "firmware_upgrade.success",
          "is_read": 0,
          "messge": "{ring_name}有新版韌體更新成功",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z"
          },
          "timestamp": "2016-10-12T15:30:15Z"
        },
        {
          "id": 7,
          "type": "firmware_upgrade.fail",
          "is_read": 0,
          "messge": "{ring_name}有新版韌體更新失敗",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 1,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z"
          },
          "timestamp": "2016-10-12T15:30:15Z"
        },
        {
          "id": 8,
          "type": "no_signal",
          "is_read": 0,
          "messge": "{ring_name}無訊號已超超過6小時",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z",
            "last_location": {
              "ring_sn": "ring_name",
              "type_code": "L0",
              "longitude": 25.123123,
              "latitude": 102.12312312,
              "type": "gps",
              "battery_power": 5,
              "timestamp": "2016-10-09T15:30:15Z"
            }
          },
          "timestamp": "2016-10-12T15:30:15Z"
        },
        {
          "id": 9,
          "type": "app_upgrade.new",
          "is_read": 0,
          "messge": "APP有新版本",
          "upgrade_data": {
            "uid": "string",
            "nickname": "string",
            "img_path": "string",
            "platform": "android",
            "ring_data": [{
              "ring_name": "ring_name",
              "ring_sn": "12345678901",
              "firmware_version": 100,
              "firmware_upgrade_flag": 0,
              "contact_number": "string",
              "provision_status": "activated",
              "mode": "normal",
              "create_time": "2016-10-09T15:30:15Z"
            }]
          },
          "timestamp": "2016-10-12T15:30:15Z"
        },
        {
          "id": 10,
          "type": "end_of_service",
          "is_read": 0,
          "messge": "{ring_name}服務到期",
          "ring_data": {
            "ring_name": "ring_name",
            "ring_sn": "12345678901",
            "firmware_version": 100,
            "firmware_upgrade_flag": 0,
            "contact_number": "string",
            "provision_status": "activated",
            "mode": "normal",
            "create_time": "2016-10-09T15:30:15Z"
          },
          "timestamp": "2016-10-12T15:30:15Z"
        }
      ],
      "message": "success"
    }
