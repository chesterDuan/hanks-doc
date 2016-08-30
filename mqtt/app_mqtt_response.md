mqtt location messsage body
===

1. 定位 topic

        hanks ap publish => clientId/location/ringSN,
        
        app sub => clientId/location/

2. 手環收到訊息後所回傳的response => json data

3. 定位實際所回傳的 location response:(特例: 手環定位失敗, 也算是回傳成功訊息, 但APP可由message來判斷相關錯誤.)

    2016.08.26 NOTE: 
      
        現在不管是定位成功或是失敗都會統一回傳下列資料結構.
        且成功為回傳最近的一筆定位資料
        失敗, 則Server會回傳最後(新)一筆的定位資料
    
    
    mqtt response format

   
        {
            "data" : {
                "ring_sn" : "ring_sn", 
                //Ring unique Id
                
                "cmd" : 1,
                //接受指令種類（gps, fence..etc)
                
                "cmd_key" : "1qazxsw22",  
                // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.
                
                "longitude" : 25.12312, 
                // Double
                
                "latitude" :  26.12312,         
                // Double
                
                "timestamp" : "2002-10-02T15:00:00Z",  
                // String (RFC3339 normalize to UTC) => server get timestamp
                
                "type" : "gps",                 
                // String(gps/rrc_indoor/rrc_outdoor)
                
                "ring_response_code" : 0
                // 1: 定位成功 / 0:定位失敗 => 定位失敗, 如手環有回傳訊息, 可是返回APP中, 其中某一環節.
            },
            "message" : "success" 
        }    
        
       
     mqtt cmd response format  
     
        {  
            "data" : {  
            
                "ring_sn" : "ring_sn",   
                // Ring unique Id  
                
                "cmd" : 1,  
                //接受指令種類（gps, fence..etc)  
                
                "cmd_key" : "1qazxsw22",  
                // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.  
                
                "fence_no" : 1  // 1 ~ 5    
                
                "timestamp" : "2002-10-02T15:00:00Z",  
                // String (RFC3339 normalize to UTC) => server get timestamp
                
                "ring_error_code" : 0  
                // 1: 手環指令成功 / 0:手環指令失敗
                
            },  
            "message" : "success"   
        }    
        


4. 設定fence後回傳的response:

    SUCCESS:
   
        {
          "data" : {
              "ring_sn" : 
              "cmd":
              "cmd_key" : "1qazxsw22"   // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.
              "fence_no" :          
              "timestamp" :     // String (RFC3339 normalize to UTC) => server get timestamp
              "ring_response_code" : 0       // 1: 定位成功 / 0:定位失敗 => 定位失敗, 如手環有回傳訊息, 可是返回APP中, 其中某一環節.
          },
          "message" : "success" 
        }
  
    FAIL:
    
        {
            "error" : {
                "err_code" : "server statusCode",
                "err_message" : "Something goes wrong!!"
            } 
        }
  
5. 手環收到cmd後所回傳的資料, 也是先由hanks-spark收下來後, 再publish到app上:

    目前和APP有關return cmd:
    
        定時更新 && 電子柵欄設定 二個
        
        即時更新和主動追踪, 都是直接回手環定位資料, 不會回return cmd.

    SUCCESS:
    
        {
          "data" : {
              "ring_sn" : 
              "cmd":
              "cmd_key" : "1qazxsw22"   // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.
              "cmd_result" :     // 0=fail, 1=OK
              "cmd_error" :      // 0=no error, 1=?, 2=?, ....(待確定錯誤類別)
              "timestamp" :      // String (RFC3339 normalize to UTC) => server get timestamp
          },
          "message" : "success" 
        }  

     FAIL:
    
        {
            "error" : {
                "err_code" : "server statusCode"
                "err_meaasge" : "something error"
            } 
        }

6. 定位狀態變換:

    model = normal, active, fence

---before web resp--after web resp---receive mqtt----- data flow status

    gps -> idle -> busy -> idle, mode = normal
    
    active/on -> idle -> busy -> idle(active) 
    
    active/off -> idle -> busy(active) -> idle(normal)