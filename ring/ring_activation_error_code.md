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
        
6. 簡訊驗證碼輸入錯誤

         {
           "error": {
             "err_code": "000025",
             "err_message": "ring captcha input number is invalid"
           }
         }

7. 簡訊驗證碼輸入錯誤超過3次

         {
           "error": {
             "err_code": "000026",
             "err_message": "ring captcha input invalided is over three times"
           }
         }



7. 簡訊驗證碼顏率過高(待定義)