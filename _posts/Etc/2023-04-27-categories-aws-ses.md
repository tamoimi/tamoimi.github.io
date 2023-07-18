---
title: "[AWS-SES, Next.js] AWS SES와 Next.js를 사용해 이메일 보내기"
categories:
  - AWS
tags:
  - [AWS, AWS-SES, Next.js]

permalink: /Blog/aws-ses/
toc: true
toc_sticky: true
toc_label: # "AWS-SES"
date: 2023-04-27
last_modified_at: 2023-04-27
---

## Amazon SES란?

사용자의 이메일 주소와 도메인을 사용해 SMTP방식과 API방식으로 이메일을 보내고 받기 위한 경제적이고 손쉬운 방법을 제공하는 아마존의 이메일 플랫폼.

## 작동방식

1. 이메일 발신자 쪽에서 Amazon SES에게 하나 이상의 수신자에게 이메일을 전송하는 요청을 보낸다.
2. 요청이 유효하면 Amazon SES가 이메일을 수락한다.
3. Amazon SES는 인터넷을 통해 수신자의 수신 장치에 메시지를 보낸다.
4. 이 시점에서 다양한 가능성이 존재합다.
   - ISP가 성공적으로 메시지를 수신자의 수신함으로 전송한다.
   - 수신자의 이메일 주소가 존재하지 않음. 따라서 ISP가 Amazon SES로 반송 메일 알림을 전송한다.
   - 수신자가 메시지를 수신하지만 이를 스팸으로 여겨 ISP에게 수신 거부를 제기한다.

## 적용 방법

- AWS SDK for JavaScript 설치: Next.js 애플리케이션에서 SES 서비스를 사용하려면 AWS SDK for JavaScript를 설치해야 한다. npm이나 yarn을 사용하여 다음 명령어를 터미널에서 실행할 수 있다.

```js
// AWS SDK (software development kit) aws-sdk/client-ses 설치
npm install @aws-sdk/client-ses
```

- 프로젝트의 루트 디렉터리에 .env 파일을 만들고 AWS 자격 증명을 추가한다.

```js
AWS_ACCESS_KEY_ID = YOUR_ACCESS_KEY_ID;
AWS_SECRET_ACCESS_KEY = YOUR_SECRET_ACCESS_KEY;
AWS_REGION = YOUR_REGION;
```

- AWS 연동하기

```js
import { SESClient } from "@aws-sdk/client-ses";

const sesClient = new SESClient({
region: process.env.AWS_REGION!,
credentials: {
   accessKeyId: process.env.AWS_ACCESS_KEY_ID!,
   secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY!
}
});
export { sesClient };
```

- API 작성

```js
import { sesClient } from "@/libs/sesClient";
import { SendEmailCommand } from "@aws-sdk/client-ses";

const emailHandler = async () => {
  try {
    const emailResponse = await sesClient.send(
      new SendEmailCommand({
        Destination: {
          ToAddresses: [
            // Email_receiver
          ],
          CcAddresses: [],
        },
        Message: {
          Body: {
            Text: {
              Charset: "UTF-8",
              Data: "EMAIL TEST",
            },
          },
          Subject: {
            Charset: "UTF-8",
            Data: "AWS SES 테스트",
          },
        },
        Source: // Email sender
      })
    );

    console.log("Real Email sent successfully:", emailResponse);
  } catch (err) {
    console.error("Error sending email:", err);
  }
};

export default emailHandler;
```

- 원하는 페이지, 컴포넌트에서 api를 호출 하면 끝
![image](https://user-images.githubusercontent.com/129496536/234804894-f1de018b-60db-47db-9988-b5a5e0b281de.png)

+ 내용이 부실하기 때문에 나중에 추가할 것 😥
