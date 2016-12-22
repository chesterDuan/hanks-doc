APP 強制更新流程說明
==

1. 需要在request header中加入下列資料來讓Server檢查:

     
       android:
       
        hanks-app-ver: 12
        hanks-app-platform: "android"
           
       iphone:
       
        hanks-app-ver: 12
        hanks-app-platform: "iphone"

2. 只要是URL有包含`/v1/user`, header皆要帶version和platform

3. 假如Server檢查到需要做強制更新時, 則是回`http status = 400` 

        {
          "error": {
            "err_code": "000051",
            "err_message": "app version is too old"
          }
        }

4. (TODO): Server會準備可測試的環境, 方便APP做功能測試.