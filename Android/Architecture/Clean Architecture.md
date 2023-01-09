# Clean Architecture?

-----

![post-thumbnail](https://velog.velcdn.com/images/galaxy/post/9e33b45e-75c6-464c-9a3b-3a1cdd7ef2c5/image.png)

## 👉 중요하게 생각하는 것들

- 내부 데이터와 로직들은 안쪽을 향해야 한다.
- 요청은 안쪽으로 들어와 바깥쪽으로 나간다.> 요청 진행 방향이 변화되는 경우는 존재하지 않는다.
- DI(Dependency Injection) : 인터페이스의 변경이 코드의 변화를 일으키지 않도록 한다.
- DB, UI 등은 바뀌어도 프로그램 자체는 문제 없이 돌아가도록하는 **세부 사항으로 취급**한다.

## 1.  Clean Architecture란

***\*Clean Architecture는 Robert C Martin(Uncle Bob) 제시한 소프트웨어 설계 방식이다.\****

## 2. Clean Architecture를 사용하는 이유

- **계층(Layer)별로 역할(관심사)를 나누어 분리**함으로써 **다양한 요구**(대규모 업데이트, 새로운 기능, 버그수정, 테스트, 고객의 요청)등에 **유연하게 대처**하기 위해 사용
- 이러한 계층간에 역할을 알기전에 의존성 규칙을 알아야 한다.

## 3. 의존성 규칙(Dependency Rule)

- 계층마다 경계를 나누어서 관심사를 분리하기 위해 사용하는 규칙

1)**모든 소스코드 의존성은 반드시 바깥쪽에서 안쪽으로, 고수준 정책을 향해야 한다**

- 안쪽으로 갈수록 고수준에 해당하고,

  고수준과 저수준은 추상화의 정도에 따라 분류됩니다.

- 추상화가 많이 되어있을수록 안쪽에 위치해있고 고수준에 해당합니다.

2)고수준에 있는 계층은 저수준에 있는 계층에 대해 몰라야 한다.

- 안쪽에 있는 Domain 계층은 DataLayer나 PresentationLayer에 의존하지 않고 독립적으로 실행 되어야 한다는 규칙입니다.

![img](https://velog.velcdn.com/images%2Fsery270%2Fpost%2F5537acce-99c4-4de1-8516-b3f1e7da5b85%2Fcleancoder.png)

## 4. Clean Architecture의 Layear들

> 아래 그림은 위에서 보았던 Clean Architecture 그림을 90도 회전한 모습입니다. Clean Architecture의 각 Layer들을 설명하기 위해 아래와 같이 활용되었습니다.

![img](https://velog.velcdn.com/images%2Fsery270%2Fpost%2Fbe3ae900-54b3-47c6-a4ba-03f785c7c84d%2FrotatedLayers.png)

### 📦 Presentaion Layer

> 위 그림의 Presenter를 Presenters 뿐만 아니라, ViewModels도 포괄하기 위한 말로, Controllers라고 부르겠습니돠.

- UI (*Activities & Fragments*), Controllers (*Presenters/ViewModels*) 를 포함합니다.
- Controllers (*Presenters/ViewModels*)은 1개 이상의 *Use cases*를 실행합니다.
- UI은 UI 각각의 Controllers (*Presenters/ViewModels*)에 의해 조정됩니다.
- Presentation Layer는 Domain Layer을 대상으로 의존성을 가집니다.

> Presentation Layer - - - > Domain Layer

### 🔒 Domain Layear

- *Entities, Use cases, Repository Interfaces*를 포함합니다.
- *Use cases*는 data와 1개 이상의 Repository Interfaces를 결합합니다.
- Domain Layer는 가장 안쪽의 레이어입니다. 앞서 언급한 의존성 법칙에 의해, Domain Layer는 다른 레이어를 대상으로 의존성을 가지지 않습니다. 다른 레이어가 Domain Layer를 대상으로 의존성을 가질 뿐입니다.

> 어떻게 Domain Layer는 Data Layer에 대힌 의존성도 가지지 않을 수 있나요?
>
> 한마디로 답변하자면, SOLID 원칙 중 **의존성 역전 법칙**에 해당하는 **interface를 사용한 추상화** 덕분입니다.
>
> Interface 추상화가 없었다면, Domain Layer의 Use cases가 Data Layer의 Repository를 사용해야합니다. 즉, Domain Layer - - - > Data Layer 라는 의존이 생겨나게 됩니다.
>
> 하지만 **Domain Layer는 Repository를 추상화시켜 사용**하고 있기 때문에, 위와 같은 의존이 생겨나지 않게 되는 것입니다. 즉, Domain Layer는 Data Layer에서 구현될 Repository Interfaces를 사용하면서, 의존을 회피하게 됩니다.
>
> 이것이 바로 **Repository Interfaces가 Domain Layer에 포함되는 이유**이자, **Repository Implementations가Data Layer에 포함되는 이유** 라고 볼 수 있습니다.

> **의존성 역전 법칙을 한마디로 ?**
>
> High-level modules should not depend on low-level modules, both should depend on abstractions.

### **Domain Layer**의 특징 ‼️

- Domain Layer 가장 중요한 레이어 입니다 ‼️ 따라서 다른 레이어들과는 달리, 잘 바뀌면 안됩니다.
  - 이 Domain Layer에 소프트웨어의 중심이 되는 The business rules(Entity)가 포함됩니다.
- Domain Layer는 다른 레이어를 대상으로 의존성을 가지지 않습니다.
  - 즉, Domain Layer는 프레임 워크(Android Platform)에 의존성을 가지지 않고, 오직 언어 단(Kotlin Module)에 대해서만 의존성을 갖습니다.
    - 따라서, 프레임 워크간의 Domain Layer 재사용도 가능합니다.

### **Data (DataSource) Layer**

- *Repository Implementations*, 1개 이상의 *Data Sources*를 포함합니다.

> Data Layer의 *Repository Implementations* Data Layer가 가진 책임 중 하나로, Domain Layer가 사용하는 Repository Interfaces에 대한 구현을 이야기 할 수 있습니다. Domain Layer는 Data Layer가 구현해줄거라 생각하고 Repository Interfaces를 사용했기 때문입니다.

Repository는 다른 Data Source들을 결합/조정합니다.

- Repository 여러 Data Source들을 결합하는 경우로, Local Data Source과 Remote Data Source의 결합에 대해 이야기할 수 있습니다.

> **dataSource와 dataSourceImpl**
>
> Data Layer의 Data Source도, 위에서 봤던 **의존성 역전 법칙**의 적용으로, 추상화 되어 interface와 Implementations으로 구성됩니다.즉, Repository - - -> Data Source의 의존에 대한 회피입니다.
>
> 한편, 이렇게 의존을 없애면, Data Source의 변경시, Repository에 대한 영향을 줄일 수 있습니다.

Repositroy 패턴

[[Android\] Repository Pattern](https://www.notion.so/Android-Repository-Pattern-900e3880c30c4f4f809ffe1f0852dc6a)

- Data Layer는 Domain Layer을 대상으로 의존성을 가집니다.

  > Data Layer - - - > Domain Layer