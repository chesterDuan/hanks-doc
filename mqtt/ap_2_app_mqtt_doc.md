AP to APP MQTT 說明
==

|Type Code|Description|Type Code|Description|
|----|----|----|----|
|L0|定時更新|L1|電子柵欄|
|L2|主動追踪|L3|即時定位|
|C0|門號啟動相關|C1|現在位址|
|C2|主動追踪開關|C3|電子柵欄設定|
|C5|手環軔體更新||

----

> 1. 定時更新 location => 無ack, 只有定位資訊
> 2. 即時定位 ack / location
> 3. 主動追踪ON ack / location
> 4. 主動追踪OFF ack
> 5. 電子柵欄 ack / location => 新增/編輯/刪除 ack 都一樣
> 6. 超出電子柵欄 event => 無ack, 只有定位資訊 
> 7. 登入資料 event => 確定uid正確後, 發出的login mqtt, 來達成踼除舊有裝置之event.
> 8. 虛擬門號 => 啟用成功(失敗)時, 所傳送的MQTT
> 9. 手環軔體更新 => 手環軔體更新成功 or 失敗通知

1. 定時更新   

    > location topic: `hanks/app/{clientId}/location/{ringSN}`
     
        mos_publish -q 2 -t "hanks/app/{clientId}/location/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/{ringSN}"
    
    > location mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",    // Ring unique Id
                
                "type_code" : "L0",         // 定時更新 
                
                "longitude" : 25.12312,   // Double
                
                "latitude" :  26.12312,   // Double
                
                "timestamp" : "2002-10-02T15:00:00Z",
                
                "type" : "gps",           // String(gps/rrc_indoor/rrc_outdoor)
                
                "battery_power" : 100 
                
                "ring_response_code" : 0 // 0: 定位成功 / 1:定位失敗
            },
            "message" : "success" 
        }  

2. 即時定位  

    > ack topic: `hanks/app/{clientId}/cmd/{ringSN}`
     
        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/cmd/{ringSN}"
        
     
     > ack mqtt message body:
     
        {  
            "data" : {  
            
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C1",         // 接受指令種類  
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環指令成功 / 1:手環指令失敗
                
            }
        }  
     
    
    > location topic: `hanks/app/{clientId}/location/{ringSN}`
     
        mos_publish -q 2 -t "hanks/app/{clientId}/location/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/{ringSN}"
    
    > location mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",    // Ring unique Id
                
                "type_code" : "L3",         // 即時定位 
                
                "longitude" : 25.12312,   // Double
                
                "latitude" :  26.12312,   // Double
                
                "timestamp" : "2002-10-02T15:00:00Z",
                
                "type" : "gps",           // String(gps/rrc_indoor/rrc_outdoor)
                
                "battery_power" : 100, 
                
                "ring_response_code" : 0 // 0: 定位成功 / 1:定位失敗
            },
            "message" : "success" 
        }  
    
3. 主動追踪 ON   

    > ack topic: `hanks/app/{clientId}/cmd/{ringSN}`

        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/cmd/{ringSN}"
   
    > ack mqtt message body:
    
        {  
            "data" : {  
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C2",        // 主動開關
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環指令成功 / 1:手環指令失敗
            }
        }  
   
    > location topic: `hanks/app/{clientId}/location/{ringSN}`

        mos_publish -q 2 -t "hanks/app/{clientId}/location/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/{ringSN}"
    
    > location mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",   // Ring unique Id
                
                "type_code" : "L2",        // 主動追踪
                
                "longitude" : 25.12312,  // Double
                
                "latitude" :  26.12312,  // Double
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "type" : "gps",          // String(gps/rrc_indoor/rrc_outdoor)
                
                "battery_power" : 100 
                
                "ring_response_code" : 0   // 0: 定位成功 / 1:定位失敗
            },
            "message" : "success" 
        } 
   
4. 主動追踪 OFF  

    > ack topic: `hanks/app/{clientId}/cmd/{ringSN}`

        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/cmd/{ringSN}"
   
    > ack mqtt message body:
    
        {  
            "data" : {  
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C2",        // 主動開關
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環指令成功 / 1:手環指令失敗
            }
        }  

5. 電子柵欄 ack / location => 新增/編輯/刪除 ack 都一樣

    > ack topic: `hanks/app/{clientId}/cmd/{ringSN}`

        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{.....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/cmd/{ringSN}"
   
    > ack mqtt message body:
    
        {  
            "data" : {  
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C3",        // 電子柵欄設定
                
                "fence_no" : [1,2,3]           // 電子柵欄編號 1 ~ 5
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環指令成功 / 1:手環指令失敗
            }
        } 
        
    > location topic: `hanks/app/{clientId}/location/{ringSN}`

          mos_publish -q 2 -t "hanks/app/{clientId}/location/{ringSN}" -m "{.....}"
        
          mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/location/{ringSN}"
    
    > location mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",   // Ring unique Id
                
                "type_code" : "L1",        // 電子柵欄
                
                "fence_no" : 1           // 電子柵欄編號 1 ~ 5
                
                "longitude" : 25.12312,  // Double
                
                "latitude" :  26.12312,  // Double
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "type" : "gps",          // String(gps/rrc_indoor/rrc_outdoor)
                
                "battery_power" : 100 
                
                "ring_response_code" : 0   // 0: 定位成功 / 1:定位失敗
            },
            "message" : "success" 
        } 
        
6. 超出電子柵欄 location => 無ack, 只有定位資訊

    > location topic: `hanks/app/{clientId}/event/{ringSN}`

        mos_publish -q 2 -t "hanks/app/{clientId}/event/{ringSN}" -m "{參考_即時定位_location_data}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/event/{ringSN}"
    
    > location mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",   // Ring unique Id
                
                "type_code" : "L1",        // 電子柵欄
                
                "fence_no" : 1           // 電子柵欄編號 1 ~ 5
                
                "out_of_fence" : 1       // 超出電子柵欄 FLAG
                
                "longitude" : 25.12312,  // Double
                
                "latitude" :  26.12312,  // Double
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "type" : "gps",          // String(gps/rrc_indoor/rrc_outdoor)
                
                "battery_power" : 100 
                
                "ring_response_code" : 0 // 0: 定位成功 / 1:定位失敗
            },
            "message" : "success" 
        } 
        
7. 登入資料 forcelog => 確定uid正確後, 發出的login mqtt, 來達成踼除舊有裝置之動作.

     > forcelog topic: `hanks/app/{clientId}/forcelogout`

        mos_publish -q 2 -t "hanks/app/{clientId}/forcelogout" -m "{請參考message_body}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/forcelogout"  
        
    > event mqtt message body:
    
        {
            "data" : {
                
                "phone_model" : "nexus_5x",  // 手機型號
                
                "platform" : "android",
                
                "app_ver" : 100,

                "last_login" : "2016-09-22T15:16:35Z",
                
            },
            "message" : "success" 
        } 
        
8. 虛擬門號 => 啟用成功(失敗)時, 所傳送的MQTT

    > virtual number topic: hanks/app/{clientId}/cmd/{ringSN}
   
        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{請參考message_body}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}
   
    > cmd mqtt message body (成功):  
        
         {
            "data" : {
                "ring_sn" : "ring_sn",    // Ring unique Id
        
                 type_code : C0,          // 手環啟動
        
                "longitude" : 25.12312,   // Double
        
                "latitude" :  26.12312,   // Double
        
                "timestamp" : "2002-10-02T15:00:00Z",
        
                "type" : "gps",           // String(gps/rrc_indoor/rrc_outdoor)
        
                "battery_power" : 100, 
        
                "ring_response_code" : 0 // 0: 啟用成功
            },
            "message" : "success" 
        }
        
    > cmd mqtt message body (失敗):  
        
         {
            "data" : {
                "ring_sn" : "ring_sn",    // Ring unique Id
        
                 type_code : C0,          // 手環啟動
        
                "timestamp" : "2002-10-02T15:00:00Z",
        
                "ring_response_code" : 1 // 1:啟用失敗
            },
            "message" : "success" 
        }
        
9. 手環軔體更新 => 手環軔體更新成功 or 失敗通知

     > firmware upgrade topic: `hanks/app/{clientId}/cmd/{ringSN}`
     
        mos_publish -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}" -m "{....}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/cmd/{ringSN}"
        
     
     > mqtt message body:
     
        {  
            "data" : {  
            
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C5",         // 接受指令種類  
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環軔體更新成功 / 1: 軔體更新失敗(手環電量過低) / 2: 軔體更新失敗(其它錯誤)
                
            }
        }  

      > event firmware topic: `hanks/app/{clientId}/event`

        mos_publish -q 2 -t "hanks/app/{clientId}/event/{ringSN}" -m "{參考_即時定位_location_data}"
        
        mos_subscribe -c -i "{clientId}" -q 2 -t "hanks/app/{clientId}/event/{ringSN}"
    
      > event firmware mqtt message body:
    
        {
            "data" : {
                "ring_sn" : "ring_sn",   // Ring unique Id  
                
                "type_code" : "C5",         // 接受指令種類  
                
                "timestamp" : "2016-08-02T15:00:00Z",
                
                "ring_response_code" : 0  // 0: 手環軔體更新成功 / 1: 軔體更新失敗(手環電量過低) / 2: 軔體更新失敗(其它錯誤)
            },
            "message" : "success" 
        } 
        
        