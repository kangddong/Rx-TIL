## Message

<details>
  <summary> 2023.02.04 신규 프로젝트의 경우 FCM API(v1) 사용 필수 </summary>
  
  ## FCM 레거시 HTTP API를 사용해서 보내기
  
  ```
    https://fcm.googleapis.com/fcm/send
    Content-Type:application/json
    Authorization:key=AIzasSyZ-.....asdasdA
    
    { "data": {
        "name" : "Rx",
        "age" : 28,
      },
      "to" : "",
      "direct_boot_ok" : true
    }
  ```
  
  ## FCM v1 HTTP API를 사용하여 보내기
  
  ```
    https://fcm.googleapis.com/v1/projects/<project-name>/messages:send
    Content-Type:application/json
    Authorization:Bearer ya29.AIzasSyZ-.....asdasdA
    
    {
      "message": {
        "token" : "asdasdasdasda..."
        "data": {
          "name" : "Rx",
          "age" : 28,
        },
        "android": {
          "direct_boot_ok" : true
        },
      }
   }
 ```
  
</details>
  
