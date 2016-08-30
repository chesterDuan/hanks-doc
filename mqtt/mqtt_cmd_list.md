mqtt_cmd_list
===

#### CMD Type
|Type|Description|Type|Description|
|----|----|----|----|
|1|即時定位|2|主動追踪|
|3|電子柵欄|4|定時更新|
|5|FW check|6|FW 更新|
|7|健康檢查|8|GPS behavior config|
|9|上傳位置更新 time out behavior config.||

---


1. 定時更新
   
    Ap to APP
    
    定時更新 return publish cmd   
    
    MQTT cmd response Topic `hanks/app/{clientId}/cmd/{ringSN}/4`
     
        mos_publish -q 2 -t "hanks/app/clientId/location/routine/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/routine/ringSN"
        
     定時更新: 定位資訊 cmd:
     
     MQTT 定位資料 Topic `hanks/app/{clientId}/location/{ringSN}/4`
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/routine/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/routine/ringSN"
    
    Ring to AP (TODO)

2. 即時定位

    Ap to APP
   
      即時定位 return publish cmd(未確定)
      
      MQTT cmd response Topic `hanks/app/{clientId}/cmd/{ringSN}/1`
     
        mos_publish -q 2 -t "hanks/app/clientId/location/gps/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/gps/return/ringSN"
        
     即時定位, 定位資訊 cmd:  
     
     MQTT Topic `hanks/app/{clientId}/location/{ringSN}/1`
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/gps/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/gps/ringSN"
    
    Ring to AP (TODO)
      
      
3. 主動追踪

    Ap to APP
   
    主動追踪 return publish cmd(未確定)
    
    MQTT cmd response Topic `hanks/app/{clientId}/cmd/{ringSN}/2`
     
        mos_publish -q 2 -t "hanks/app/clientId/location/active/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/active/return/ringSN"
        
     主動追踪 , 定位資訊 cmd:
     
     MQTT Topic `hanks/app/{clientId}/location/{ringSN}/2`
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/active/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/active/ringSN"
    
   
    
    Ring to AP (TODO)
    
