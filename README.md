# NGUIZ

NGUIZ is an application that allows users to hunt quizzes in public places. Users can work on quizzes with attractive prizes every week.

## SYSTEM & INFRACTRUCTURE

### SERVER

Free base.

### DATABASE

This app using non sql database which is this app using mongodb.

### BACKEND

This app using NodeJS with express js framework as backend. This backend uses a model-controller architecture.

### FRONTEND

This app using React with next js framework as frontend. This frontend using modular architectire.

## REQUIREMENT

### DESIGN SYSTEM

#### FLOWCHART

```mermaid
flowchart TB
  start([START])
  step1[SCAN THE QR]
  auth((AUTH))
  step2[OPEN THE QUIZ]
  step3[DO THE QUIZ]
  step4[GET THE RESULT]
  finish([FINNISH])

  auth_start((AUTH))
  auth_step1[LOGIN]
  auth_step2[REGISTER]
  auth_is_logged_in{is logged in}
  auth_has_register{has register}
  auth_finish((AUTH))

  auth_start-->
    auth_is_logged_in-->|yes|auth_finish
    auth_is_logged_in-->
      |no|auth_has_register
      auth_has_register-->|yes|auth_step1
      auth_has_register-->|no|auth_step2-->auth_step1
    auth_step1-->auth_finish

  start-->step1-->auth-->step2-->step3-->step4-->finish
```

#### SERVICES

```mermaid
---
title: AuthService
---
flowchart LR
  classDef Actor fill:#ECFFEC,stroke:#70DB7C,color:#19A428;
  classDef Service fill:#E8FFF5,stroke:#70D6DB,color:#2AC5CD;
  classDef Flow fill:#26220D,stroke:#AC9939,color:#BFAA40;

  public[PUBLIC]:::Actor
  admin[ADMIN]:::Actor

  AuthService[(AuthService)]:::Service

  subgraph PUBLIC
    public
  end

  subgraph ADMIN
    admin
  end

  subgraph SERVICE
    AuthService
  end

  public<-->|get::me|AuthService
  public-->|post::login|AuthService
  public-->|post::register|AuthService
  admin<-->|get::me|AuthService
  admin-->|post::login|AuthService
```

```mermaid
---
title: QuizService
---
flowchart LR
  classDef Actor fill:#ECFFEC,stroke:#70DB7C,color:#19A428;
  classDef Service fill:#E8FFF5,stroke:#70D6DB,color:#2AC5CD;
  classDef Flow fill:#26220D,stroke:#AC9939,color:#BFAA40;

  public[PUBLIC]:::Actor
  admin[ADMIN]:::Actor

  QuizService[(QuizService)]:::Service

  subgraph PUBLIC
    public
  end

  subgraph ADMIN
    admin
  end

  subgraph SERVICE
    QuizService
  end

  public<-->|get::detail|QuizService
  public-->|post::start|QuizService
  public-->|post::submit|QuizService
  public<-->|get::result|QuizService
  public<-->|get::leaderboard|QuizService

  admin<-->|get::list|QuizService
  admin<-->|get::detail|QuizService
  admin-->|post::create|QuizService
  admin-->|patch::update|QuizService
  admin-->|patch::publish|QuizService
  admin-->|patch::archive|QuizService
  admin-->|delete::delete|QuizService
```

```mermaid
---
title: QuestionService
---
flowchart LR
  classDef Actor fill:#ECFFEC,stroke:#70DB7C,color:#19A428;
  classDef Service fill:#E8FFF5,stroke:#70D6DB,color:#2AC5CD;
  classDef Flow fill:#26220D,stroke:#AC9939,color:#BFAA40;

  public[PUBLIC]:::Actor
  admin[ADMIN]:::Actor

  QuestionService[(QuestionService)]:::Service

  subgraph PUBLIC
    public
  end

  subgraph ADMIN
    admin
  end

  subgraph SERVICE
    QuestionService
  end

  public<-->|get::detail|QuestionService

  admin<-->|get::detail|QuestionService
  admin-->|post::create|QuestionService
  admin-->|patch::update|QuestionService
  admin-->|delete::delete|QuestionService
```
