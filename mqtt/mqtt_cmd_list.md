mqtt_cmd_list
===

1. 定時更新
   
    Ap to APP
    
    定時更新 return publish cmd
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/routine/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/routine/ringSN"
        
     定時更新: 定位資訊:
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/routine/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/routine/ringSN"
    
   Ring to AP (TODO)

2. 即時定位

   Ap to APP
   
      定時更新 return publish cmd(未確定)
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/gps/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/gps/return/ringSN"
        
     定時更新, 定位資訊:
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/gps/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/gps/ringSN"
    
   Ring to AP (TODO)
      
      
3. 主動追踪

    Ap to APP
   
    定時更新 return publish cmd(未確定)
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/active/return/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/active/return/ringSN"
        
     定時更新, 定位資訊:
     
        mos_publish -r -q 2 -t "hanks/app/clientId/location/active/ringSN" -m "待定義"
        
        mos_subscribe -c -i "clientId" -q 2 -t "hanks/app/clientId/location/active/ringSN"
    
   
    
   Ring to AP (TODO)