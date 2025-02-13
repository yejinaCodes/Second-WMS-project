# 3PL
<p align="center"><img width="423" alt="image" src="https://github.com/user-attachments/assets/166dc043-a8b9-4264-aefd-d45a6c2913fa"></p>

Warehouse Management System aims to enhance inventory management, streamline stock control, and improve admin management features.

<img width="413" alt="singlehousehold" src="https://github.com/user-attachments/assets/b296ef86-4392-48f6-a77d-4052f2aabf68" />

With the increasing number of single-person households, there is a growing demand for space-efficient furniture that is both practical and personalized. To align with this trend, we have developed a project that provides warehouse rental services for storing a variety of furniture products designed to meet the needs of single-person households.

Our WMS project is a back-office system aimed at reducing operational costs and improving accuracy through warehouse inventory management and automated inbound and outbound processes.

## TEAM
|                                                                                   **김예진**                                                                                 |                    **AAA**                     |                **BBB**                 |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------:|:--------------------------------------:|
| Outbound Management, Dispatch Management, Notion Management | Member/Admin Management, Inbound Management, Github Management | Warehouse Management, Inventory Management |
<br>

## WORK BREAKDOWN STRUCTURE
<img width="301" alt="wbs2" src="https://github.com/user-attachments/assets/ebab3d30-11b4-49b1-a06f-f4890ad7a4dd" />

Our project was carried out over a one-week period.

## 1. PROJECT GOALS

- Build a fast and efficient web application development environment using **Spring Boot**.
- Simplify database interactions using **MyBatis**.
- Dynamically generate HTML on the server side using **Thymeleaf**.
- Integrate Spring Boot and Thymeleaf via **APIs** for seamless client-server data communication.
- Improve code quality and develop a stable web application through **TDD** (Test-Driven Development).

  
<br>

## 2. SYSTEM FLOW DETAILS

<img width="655" alt="systemflow1" src="https://github.com/user-attachments/assets/a48aa2e6-7cae-4632-8931-999e2d56477f" />

<img width="936" alt="systemflow2" src="https://github.com/user-attachments/assets/ec795336-a633-4272-8ad3-2e0c43338be5" />


The **Inbound** and **Outbound** processes are as follows. When a customer submits an inbound request, it is added to the request list. Once the request is approved, the goods are delivered to the warehouse. After inspection, the goods are stored in the designated locations within the warehouse. Once all procedures are complete, the system marks the inbound process as complete. When a customer submits an outbound request, it is added to the request list. Since one vehicle handles multiple outbound requests, the dispatch is approved first. After picking, inspection and loading the item, the outbound status is updated to "shipped." After the goods are delivered, vehicle returns to the warehouse, and the allocated quantities of the vehicle are reset.

For more detail please refer to my blog:
[**BLOG LINK 🔗**](https://velog.io/@lightamericano/%EC%B0%BD%EA%B3%A0-%EA%B4%80%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9CWMS-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-2%EC%B0%A8)

## 3. PACKAGE STRUCTURE
<img width="196" alt="ps" src="https://github.com/user-attachments/assets/109a9a61-d4f4-41a6-b324-41333d7f2eb5" />

**common:** Package for managing commonly used constants such as Errocode and User Status.

**config:** Package for managing the application's configuration files.

**controller:** Package that handles user requests and calls business logic to return the results. Includes a api controller package that handles REST API requests and a web controller package that handles requests related to rendering the view.

**domain:** Package for managing database entities.

**dto:** Package for managing data transfer objects. Includes request DTO package for request data sent from the client to the server and response DTO package for response data sent from the server to the client.

**exception:** Package for handling exceptions that occur in the application.

**mapper:** Package for managing MyBatis mapper interfaces.

**service:** Package for managing service interfaces that handle business logic. Includes serviceImpl package for managing implementations of service interfaces.

**mybatis:** Package for managing MyBatis-related configuration files and mapper XML files.


## 4. FEATURE IMPLEMENTATION
<img width="550" alt="wms2imp" src="https://github.com/user-attachments/assets/04ae2994-e395-4d39-a2cd-f9372a83582c" />

<img width="550" alt="wms2featimpl2" src="https://github.com/user-attachments/assets/6588222e-e4d8-4453-948c-4e8d1aba0610" />


My Role) Outbound management, Dispatch management, Notion documentation, Meeting coordination, Planning and documentation.

The **overall process flow**:
User outbound request → Admin dispatch registration → Delivery driver approval → Admin outbound approval → Outbound completion(after picking & packaging) → Delivery → Vehicle return

Implemented the following:

**Outbound List Page**
- Search filters based on warehouse-specific dispatch status, outbound approval status, and outbound period.

**Outbound Details Page**
- Outbound approval, completion, and rejection for dispatch-approved requests

Upon Outbound approval:
- logs the event in the OutboundApproval table
- Delivery status is set to PENDING.
- Conducts picking and packaging. Before 'complete' Outbound can be cancelled.

Upon Outbound completion:
- logs the event in the OutboundApproval table
- Outbound record is stored in the StockLog table.
- Waybills are registered

**Dispatch Management:**
- Dispatch registration and its associated status update trigger (APPROVED) are wrapped in a transaction
- When dispatch is registered, it is immediately approved (an additional delivery driver approval step is planned for later)
- Transactions ensure rollback consistency, meaning any operations executed by a trigger are also rolled back if needed
- Dispatch allocation capacity is increased accordingly
- Dispatch modifications have not been implemented

**Vehicle Management:**
- vehicle list retrieval
dispatch allocation per vehicle (Our WMS uses 13-ton, 18-ton, and 24-ton cargo trucks)
- If the vehicle load exceeds 80% or loading started three days prior, a "Start Delivery" trigger updates the delivery status to IN_DELIVERY for all relevant vehicle_id entries in the Delivery table

## 5. TROUBLE SHOOTING
**Issue:** Ensuring Persistence in completeOutbound Transaction.
- When executing completeOutbound(), all operations including approval logging were part of the same transaction.
- If any error occurred later in the process, a rollback would erase all changes, including outbound approval logs, which must always be retained.

**Solution:** Created separate transaction for each, completely separate from the original transaction.
- It ensures log persistence regardless of transaction rollback.
```
@Transactional(propagation = Propagation.REQUIRES_NEW)
```

## 6. DOCUMENTATIONS
[ERD Cloud](https://www.erdcloud.com/d/7XnkXuQA3TLzzmJ4X)
<br><br>

## USECASE
### 회원 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/695fad69-ae39-463d-bbaf-aadf6d68220a">

### 창고 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/6d186594-5888-430a-be5d-d8320da1743f">


### 입고 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/3f237037-5ac8-4f22-8995-c60289bd6940">

### 출고 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/e8005f08-8498-4884-9464-169b17cc4d57">


### 차량 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/8cb019f4-9850-4baa-a334-bbe92ec671be">


### 재고 관리
<img width="350" alt="image" src="https://github.com/user-attachments/assets/6c0a7040-7597-4751-99f1-8299d8f3479e">


## TECH STACK
<div align=center> 
  <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white">
    <img src="https://img.shields.io/badge/springboot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"> 
  <br>
  
  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"> 
  <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white"> 
  <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> 
  <br>

  <img src="https://img.shields.io/badge/thymeleaf-005F0F?style=for-the-badge&logo=thymeleaf&logoColor=white">
<img src="https://img.shields.io/badge/bootstrap-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white">
  <br>

<img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <br>

  <img src="https://img.shields.io/badge/notion-000000?style=for-the-badge&logo=notion&logoColor=white">
  <img src="https://img.shields.io/badge/discord-80247B?style=for-the-badge&logo=discord&logoColor=white">
  <img src="https://img.shields.io/badge/slack-4A154B?style=for-the-badge&logo=slack&logoColor=white">
  <img src="https://img.shields.io/badge/Google Drive-1DBF73?style=for-the-badge&logo=Google Drive&logoColor=white">
<br>

<img src="https://img.shields.io/badge/draw.io-F08705?style=for-the-badge&logo=diagrams.net&logoColor=white">
<img src="https://img.shields.io/badge/ERDCloud-000000?style=for-the-badge&logo=icloud&logoColor=white">

<img src="https://img.shields.io/badge/figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">
<img src="https://img.shields.io/badge/postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white">
</div>

|기술|버전|
|------|---|
|JAVA|17|
|SpringBoot|3.1.1|
|Thymeleaf|3.1.0|
|BootStrap|5.3.3|
|MySQL|8.0.21|


## 💻 구현 기능
### 회원 관리
- **[직원]** 직원이 등록 되어 있으면 담당 창고 관리자가 직원의 권한을 관리할 수 있습니다.
- **[회원]** 회원이 가입을 진행하면 `가입 승인 대기` 상태로 데이터가 생성됩니다. 직원이 회원의 정보를 확인한 후 `승인` 상태로 변경해야 가입이 완료됩니다.

### 창고 관리
- 창고 등록, 수정, 조회 등의 기능을 이용할 수 있으며, 카카오 지도 API를 활용하여 창고의 위치를 실시간으로 확인할 수 있습니다.

### 입고 관리
- 유저가 입고 요청을 하면 `입고 승인 대기` 상태로 데이터가 생성됩니다. 관리자가 입고 내용을 확인 후 `입고 승인`을 하면 창고로 상품이 입고됩니다. 상품이 문제 없이 창고에 적재 되면 관리자는 `입고 완료` 상태로 변경 하게 되고 재고 로그에 입고 데이터가 추가됩니다.

### 출고 관리
- 배차 등록이 완료된 후, 출고 승인 및 출고 완료 단계를 차례로 진행합니다. 이미 등록된 배차는 출고 승인이 되지 않은 경우에 한해 수정이나 취소가 가능합니다. 배차 등록 시 차량을 선택하고, 해당 차량의 배차 할당량을 확인합니다. 출고 요청 물품의 총 부피를 계산한 후 배차 승인이 이루어지면 차량의 할당량이 업데이트됩니다. 출고 완료 후에는 출고 상태값 업데이트 및 재고 로그 추가가 진행되며, 문제가 발생할 경우 전체 프로세스를 일관되게 유지하기 위해 출고 완료부터 하나의 트랜잭션으로 관리됩니다.

### 차량 관리
- 가구 창고 시나리오에 맞춰 13톤, 18톤, 24톤 카고 차량을 선택했습니다. 차량의 할당량이 80%를 초과하거나 배차 날짜가 당일 기준으로 3일 전인 경우, 해당 차량에 할당된 출고 요청의 승인 및 완료 여부를 확인하고 경고 메시지를 발송하는 배송 정책을 정의했습니다.

### 재고 관리
- 재고 무결성 관리를 위해 입출고 시 SQL 트리거를 사용하여 재고를 자동으로 업데이트합니다. 또한, 실사 조회 후 실제 재고를 입력할 수 있는 수정 기능과 상품 상세 조회를 통해 상품의 QR 코드 및 입출고 내역 로그를 확인할 수 있어, 상품의 입출고 시점을 파악할 수 있습니다.

## 🗣️ 회고
#### 예진 🔴
- 1차 WMS 프로젝트를 확장하며 웹 프레임워크를 활용해 백엔드와 프론트엔드 작업을 진행하게 되었습니다. 사용자 관점에서의 개발에 중점을 두었던 점이 특히 의미 있었습니다. 또한, 출고 및 배송 정책을 명확히 정의한 후에야 전체 개발을 진행해야 한다는 점과, 웹 프레임워크를 통해 프론트엔드에서 필요한 요소를 신속하게 응용하는 것이 얼마나 중요한지를 크게 깨달았습니다. 2차 프로젝트에서는 전체 서비스 제공 방식에 대한 구체적인 정책과 UI 구현을 배우며 더욱 발전할 수 있었던 경험이었습니다. 
#### 지은 🟡
- 이번 프로젝트에서는 팀원들과의 협업이 매우 중요하다는 것을 느꼈습니다. 초기 기획 단계에서부터 적극적으로 의견을 제시하고, 서로의 아이디어를 존중하며 진행할 수 있었던 점이 좋았습니다. 하지만, 프로젝트 중반에 발생한 일정 지연으로 인해 코드 리뷰 시간이 부족했던 것이 아쉬웠습니다. 앞으로는 일정 관리에 더 신경 쓰고, 미리 리뷰 시간을 확보해 품질을 높이는 데 집중할 계획입니다.
#### 태의 🟣
- 짧은 프로젝트 기간으로 인해 기능 구현을 우선시한 결과 코드 중복이 많았고, 충분한 레퍼런스를 참고하지 못했습니다. 앞으로 리팩토링을 통해 중복 코드를 줄이고 구현하지 못한 부분을 보완할 예정입니다. 또한, 코드를 다시 작성해보며 적용한 기술에 대해 깊이 있게 공부하여 원리를 파악하고자 합니다.

