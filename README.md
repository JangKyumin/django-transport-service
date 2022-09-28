# django-transport-service

### 이 프로젝트는 무엇인가?

> 짜여진 스크립트와 파라미터만 넣으면 메일을 보내도록 만들어보면 어떨까??

 위와 같이 만들어보자는 생각으로 무조건 프로젝트를 생성부터 했다. 무료로 제공되는 API를 찾아 메일 및 문자 전송 기능을 구현할 생각이지만 먼저 제공되는 것이 있는지 찾아보고 구상을 더 할 생각이다.

### 무료로 SMTP 사용하기


<details>
<summary>smtplib</summary>  

#### 소개
- google, naver 등의 SMTP 서버를 계정 연동으로 사용할 수 있다. 첨부파일도 함께 보낼 수 있기 때문에 테스트 진행 예정이다.  

### 참조
- https://docs.python.org/ko/3/library/smtplib.html
</details>

<details>
<summary>sendinblue</summary>  

#### 소개
- 무료로 하루 300개까지는 메일을 전송할 수 있다. 그 이후로는 금액을 지불해야한다.

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
