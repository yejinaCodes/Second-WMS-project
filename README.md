# 3PL
<img width="423" alt="image" src="https://github.com/user-attachments/assets/166dc043-a8b9-4264-aefd-d45a6c2913fa"></p>

Warehouse Management System aims to enhance inventory management, streamline stock control, and improve admin management features.

<img width="413" alt="singlehousehold" src="https://github.com/user-attachments/assets/b296ef86-4392-48f6-a77d-4052f2aabf68" />

With the increasing number of **single-person households**, there is a growing demand for space-efficient furniture that is both practical and personalized. To align with this trend, we have developed a project that provides warehouse rental services for storing a variety of **furniture products** designed to meet the needs of single-person households.

Our WMS project is a **back-office system** aimed at reducing operational costs and improving accuracy through warehouse stock management and automated inbound and outbound processes.

## TEAM
|                                                                                   **Yejin Kim**                                                                                 |                    **AAA**                     |                **BBB**                 |
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

## 2-1. SYSTEM FLOW DETAILS

<img width="455" alt="systemflow1" src="https://github.com/user-attachments/assets/a48aa2e6-7cae-4632-8931-999e2d56477f" />

<img width="736" alt="systemflow2" src="https://github.com/user-attachments/assets/ec795336-a633-4272-8ad3-2e0c43338be5" />


The **Inbound** and **Outbound** processes are as follows. When a customer submits an inbound request, it is added to the request list. Once the request is approved, the goods are delivered to the warehouse. After inspection, the goods are stored in the designated locations within the warehouse. Once all procedures are complete, the system marks the inbound process as complete. When a customer submits an outbound request, it is added to the request list. Since one vehicle handles multiple outbound requests, the dispatch is approved first. After picking, inspection and loading the item, the outbound status is updated to "shipped." After the goods are delivered, vehicle returns to the warehouse, and the allocated quantities of the vehicle are reset.

For more detail please refer to my blog:
[**BLOG LINK 🔗 SECTION 2**](https://velog.io/@lightamericano/%EC%B0%BD%EA%B3%A0-%EA%B4%80%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9CWMS-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-2%EC%B0%A8)


## 2-2. FEATURES
### User Management
- **[Admin]** If an employee is registered, the warehouse manager can manage their access rights.
- **[User]** When a user completes the registration process, their data is created with 'Pending Appproval' status. Admin must review the user's information and chanage the status to 'Approved' to complete the registration.

### Warehouse Management
- Users can register, update, search warehouses. The Kakao maps API is integrated to allow real-time tracking of warehouse locations.
 
### Inbound Management
- When a user submits an inbound request, the data is created with a 'Pending Inbound Approval' status. After an admin views and approves the inbound request, the product is delivered to the warehouse. Once the product is properly stored without issues, admin updates the status to 'Inbound Completed' and the inbound data is logged in the stock records.

### Outbound Management
- After dispatch registration is completed, the outbound approval and completion steps are processed sequentially. Modifications/cancellations of registered dispatches are only possible if outbound approval has not yet been granted. During registering dispatch, the user selects a vehicle and checks its allocation capacity. The total volume of the outbound request is calculated, and once the dispatch is approved, allocation is updated. Upon outbound completion, the outbound status is updated, and stock logs are recorded, To maintain consistency in the overall process, the outbound completion stage is managed as a single transaction.

### Vehicle Management
- In alignment with the furniture warehouse scenario, 13-ton, 18-ton, 24-ton cargo trucks are available. A delivery policy has been defined to send messages to admin when a vehicle's allocation exceeds 80% or when its first dispatch date is within 3 days from the current date. These messages allow the admin to check whether the assigned outbound requests have been approved and completed and are ready for delivery.

### Stock Management
- To ensure stock integrity, SQL triggers are used to automatically update inbound and outbound processes. Additionally, users can manually update stock after physical inspections. The system also allows detailed product inquiries, including QR code tracking inbound/outbound logs, enabling users to monitor the exact timeline of product movements.

## 3. TECHNOLOGY STACK

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
<img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <br>

  <img src="https://img.shields.io/badge/notion-000000?style=for-the-badge&logo=notion&logoColor=white">
<img src="https://img.shields.io/badge/draw.io-F08705?style=for-the-badge&logo=diagrams.net&logoColor=white">
<img src="https://img.shields.io/badge/ERDCloud-000000?style=for-the-badge&logo=icloud&logoColor=white">

<img src="https://img.shields.io/badge/figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">
<img src="https://img.shields.io/badge/postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white">
</div>

For detailed information: [**BLOG LINK🔗 SECTION 3**](https://velog.io/@lightamericano/%EC%B0%BD%EA%B3%A0-%EA%B4%80%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9CWMS-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-2%EC%B0%A8)

|Tech|Version|
|------|---|
|JAVA|17|
|Thymeleaf|3.1.0|
|BootStrap|5.3.3|
|MySQL|8.0.21|


## 4. PACKAGE STRUCTURE
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


## 5. FEATURE IMPLEMENTATION
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

## 6. TROUBLE SHOOTING
**Issue:** Ensuring Persistence in completeOutbound Transaction.
- When executing completeOutbound(), all operations including approval logging were part of the same transaction.
- If any error occurred later in the process, a rollback would erase all changes, including outbound approval logs, which must always be retained.

**Solution:** Created separate transaction for each, completely separate from the original transaction.
- It ensures log persistence regardless of transaction rollback.
```
@Transactional(propagation = Propagation.REQUIRES_NEW)
```

## 7. DOCUMENTATIONS
[ERD Cloud](https://www.erdcloud.com/d/7XnkXuQA3TLzzmJ4X)
<br><br>

## USECASE
### User Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/695fad69-ae39-463d-bbaf-aadf6d68220a">

### Warehouse Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/6d186594-5888-430a-be5d-d8320da1743f">


### Inbound Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/3f237037-5ac8-4f22-8995-c60289bd6940">

### Outbound Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/e8005f08-8498-4884-9464-169b17cc4d57">


### Dispatch Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/8cb019f4-9850-4baa-a334-bbe92ec671be">


### Stock Management
<img width="350" alt="image" src="https://github.com/user-attachments/assets/6c0a7040-7597-4751-99f1-8299d8f3479e">


## RETROSPECTION
- We expanded the first WMS project by utilizing a web framework to develop both the backend and frontend. After continuous modifications on policies and implementations, I realized the importance of clearly defining outbound and delivery policies before proceeding with the overall development. Through the second project, I gained valuable experience in establishing concrete policies for service delivery and refining UI implementation.
