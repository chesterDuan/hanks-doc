手環啟動 ERROR CODE 說明
==

1. 手環輸入資料不正碼

    > 手環名稱為空值

        {
          "error": {
            "err_code": "000020",
            "err_message": "ring name is empty"
          }
        }

    > 手環名稱長度(UTF-8), 中文10個字, 英文30個字. 

        {
          "error": {
            "err_code": "000020",
            "err_message": "ring name is too long"
          }
        }
        
    > 手機號碼為空值

        {
          "error": {
            "err_code": "000020",
            "err_message": "contact number is empty"
          }
        }
        
    > 手環序號為空值

        {
          "error": {
            "err_code": "000020",
            "err_message": "ring sn is empty"
          }
        }
    
2. 手環序號規則錯誤

        {
          "error": {
            "err_code": "000023",
            "err_message": "ring sn is invalid"
          }
        }

3. 手環是否已被啟用過

        {
          "error": {
            "err_code": "000021",
            "err_message": "ring is activated"
          }
        }

4. 手環是否已被其它帳號綁定

        {
          "error": {
            "err_code": "000022",
            "err_message": "ring is binding for another fetnet account"
          }
        }

5. 驗證碼輸入時間超過10分內

        {
          "error": {
            "err_code": "000024",
            "err_message": "ring captcha input time is invalid"
          }
        }
        
6. 簡訊驗證碼輸入錯誤:(times為錯誤次數)
         
    1. 輸入錯誤1次
    
            {
              "error": {
                "err_code": "000030",
                "err_message": "ring captcha input number is invalid, try the error 1 times."
              }
            }
    
    2.  輸入錯誤2次
    
            {
              "error": {
                "err_code": "000031",
                "err_message": "ring captcha input number is invalid, try the error 2 times."
              }
            }
    
    
    3.  輸入錯誤3次
    
            {
              "error": {
                "err_code": "000032",
                "err_message": "ring captcha input number is invalid, try the error 3 times."
              }
            }
    

7. 簡訊驗證碼輸入錯誤超過3次

         {
           "error": {
             "err_code": "000026",
             "err_message": "ring captcha input invalided is over three times"
           }
         }



8. 簡訊驗證碼頻率過高(如一分鐘內, 不可發request超過5次)


         {
           "error": {
             "err_code": "000028",
             "err_message": "http request is over the limit"
           }
         }
         
9. 手環數量超出上限

         {
           "error": {
             "err_code": "000033",
             "err_message": "ring count is equal 5"
           }
         }

10. 手環正在開通中


         {
           "error": {
             "err_code": "000034",
             "err_message": "ring is provisioning"
           }
         }
         
11. 沒有手環資料
         
         {
           "error": {
             "err_code": "000035",
             "err_message": "ring data is empty"
           }
         }
