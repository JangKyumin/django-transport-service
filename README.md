# django-transport-service

### 이 프로젝트는 무엇인가?

> 짜여진 스크립트와 파라미터만 넣으면 메일을 보내도록 만들어보면 어떨까??

 Django를 사용하여 메일 및 문자를 무료로 보낼 수 있는 API를 개발해보면 재미있겠다는 생각을 가지고 접근했다. 간단하게 생각한 구상은 아래와 같다.
 
<img width="761" alt="스크린샷 2022-09-29 오후 2 04 42" src="https://user-images.githubusercontent.com/21365949/192948709-0d7252b8-16ad-4c34-bad7-a375b589c449.png">

메일과 문자 전송에 필요한 정보를 간단하게 구성해봤지만 개발을 진행하며 추가로 필요한 부분을 계속 추가할 생각이다. 우선 무료로 제공되는 서비스를 먼저 찾아봐야겠다.

---
### 메일 전송


<details>
<summary>smtplib</summary>  

#### 소개
google, naver 등의 SMTP 서버를 계정 연동으로 사용할 수 있다. 첨부파일도 함께 보낼 수 있기 때문에 테스트 진행 예정이다.  

### 참조
- https://docs.python.org/ko/3/library/smtplib.html
</details>

<details>
<summary>sendinblue</summary>  

#### 소개
무료로 하루 300개까지는 메일을 전송할 수 있다. 그 이후로는 금액을 지불해야한다.

#### Example
``` python
from __future__ import print_function
import sib_api_v3_sdk
from sib_api_v3_sdk.rest import ApiException

configuration = sib_api_v3_sdk.Configuration()
configuration.api_key['api-key'] = 'YOUR API KEY'

api_instance = sib_api_v3_sdk.TransactionalEmailsApi(sib_api_v3_sdk.ApiClient(configuration))
subject = "from the Python SDK!"
sender = {"name":"Sendinblue","email":"contact@sendinblue.com"}
replyTo = {"name":"Sendinblue","email":"contact@sendinblue.com"}
html_content = "<html><body><h1>This is my first transactional email </h1></body></html>"
to = [{"email":"example@example.com","name":"Jane Doe"}]
params = {"parameter":"My param value","subject":"New Subject"}
send_smtp_email = sib_api_v3_sdk.SendSmtpEmail(to=to, bcc=bcc, cc=cc, reply_to=reply_to, headers=headers, html_content=html_content, sender=sender, subject=subject)

try:
    api_response = api_instance.send_transac_email(send_smtp_email)
    print(api_response)
except ApiException as e:
    print("Exception when calling SMTPApi->send_transac_email: %s\n" % e)
```  

#### 참조
- https://developers.sendinblue.com/recipes
- https://github.com/sendinblue/APIv3-python-library
</details>

---
### 문자 전송

<details>
<summary>twilio</summary>  

#### 소개
회원가입하면 일정 금액까지 무료로 문자 전송을 제공해주는 서비스, 이후로는 유로로 사용해야한다.

### 참조
- https://www.twilio.com/docs/libraries/python
</details>

<details>
<summary>Naver - Simple & Easy Notification Service</summary>  

#### 소개
월 50건까지는 무료로 사용 가능하다.

### 참조
- https://www.ncloud.com/product/applicationService/sens
</details>

---  

메일과 문자 전송에 관련된 부분은 좀 더 찾아볼 필요가 있을 것으로 보인다. 추가로 여러 전송 api를 찾아봤지만 대부분 비슷하게 연동되는 조건으로 사용되므로 위에 정리된 항목에서 결정하여 사용하면 될 것으로 보인다. 참고로 개인 프로젝트로 테스트에만 사용할 것이기 때문에 별도로 요금이 부과되지 않도록 조심하자!
