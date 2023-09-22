
# ios-juice-maker🧃
쥬스메이커 프로젝트 저장소입니다. 

## 목차⚡
- [기간](#기간calendar)
- [팀원](#팀원busts_in_silhouette)
- [실행 화면](#실행-화면desktop_computer)
- [실행 영상](#실행-영상clapper)
- [스토리보드](#스토리보드clipboard)
- [파일 구조](#파일-구조file_folder)
- [파일 설명](#파일-설명bookmark_tabs)
- [흐름도](#흐름도ocean)
- [고민했던점 및 궁금했던점](#고민했던점 및 궁금했던점interrobang)

<br><br>

## 기간:calendar:
2023.09.11 ~ 2023.09.27

<br><br>

## 팀원:busts_in_silhouette: 
| 프로필 사진 | <a href="https://github.com/newJunsung"><img src="https://avatars.githubusercontent.com/u/107932188?v=4" width="90" height="90"></a> | <a href="https://github.com/shlim0"><img src="https://avatars.githubusercontent.com/u/46235301?v=4" width="90" height="90"></a> |
| ---- | ----------- | --------- |
| in Github | [@newJunsung](https://github.com/newJunsung) | [@JJong](https://github.com/shlim0) |
| in SeSAC | 뉴준성 | 쫑 |

[목차로 돌아가기](#목차)
<br><br>

## 실행 화면:desktop_computer:	
- 주스 주문 화면
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 13 49 27](https://github.com/newJunsung/ios-juice-maker/assets/46235301/f0383629-a923-4ccd-bc00-79b57510b1ec)
- 주스 주문 성공 화면
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 13 49 40](https://github.com/newJunsung/ios-juice-maker/assets/46235301/691ed004-13cc-4ab4-b2b7-ebba04be57d6)
- 주스 주문 실패 화면
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 14 29 14](https://github.com/newJunsung/ios-juice-maker/assets/46235301/2ec66af7-afd8-4fae-9045-7f4faf7dd0ef)
- 과일 재고 수정 화면
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 13 51 24](https://github.com/newJunsung/ios-juice-maker/assets/46235301/7a9a63f9-dc7b-4cf4-aa22-832d706349c4)
- 과일 재고 수정 (0 ~ 100개)
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 13 51 56](https://github.com/newJunsung/ios-juice-maker/assets/46235301/d7aa3929-fe15-487a-874e-99e69e08bad6)
- 과일 재고 수정 완료 화면
![Simulator Screenshot - iPhone 15 Pro - 2023-09-22 at 13 51 58](https://github.com/newJunsung/ios-juice-maker/assets/46235301/d69b8305-a70a-4fc7-81a0-027c12ef4159)

[목차로 돌아가기](#목차)
<br><br>

## 실행 영상:clapper:	
https://github.com/newJunsung/ios-juice-maker/assets/46235301/630e7754-8fef-406b-a06c-a5bade4ecbe9

[목차로 돌아가기](#목차)
<br><br>

## 스토리보드:clipboard:	
<img width="1345" alt="image" src="https://github.com/newJunsung/ios-juice-maker/assets/46235301/89aa834f-2f42-44bb-bc2f-b59f25588d9e">

[목차로 돌아가기](#목차)
<br><br>

## 파일 구조:file_folder: 
```mermaid
classDiagram

class Protocols {
    FruitShowable.swift
}

class Controller {
  AppDelegate.swift
  FruitInvetoryViewController.swift
  JuiceMenuViewController.swift
  SceneDelegate.swift
}

class Model {
  FruitStore.swift
  FruitType.swift
  JuiceMaker.swift
  JuiceMakerException.swift
  JuiceType.swift
}

class View {
  Assets.xcassets
  LaunchScreen.stroyboard
  Main.storyboard
}
```

[목차로 돌아가기](#목차)
<br><br>

## 파일 설명:bookmark_tabs:	
- JuiceMaker
   - Protocols
      - FruitShowable: 과일 개수의 증감이 일어날 때 View에 반영합니다.
   - Controller
      - FruitInvetoryViewController: 과일 재고 수정을 합니다.
      - JuiceMenuViewController: 쥬스 메뉴의 주문을 처리합니다. 또, 주스 주문 및 과일 재고 수정을 합니다.
   - Model
      - FruitStore: 과일 개수를 조작하는 Class 입니다. 싱글톤 패턴으로 외부에서 접근할 수 있으며, `[FruitType: Int]` 타입으로 과일 개수를 저장합니다.
      - FruitType: 과일 종류를 정의합니다. 또한, `(fruitType: FruitType, count: Int)`을 `Fruit`으로 typealias 합니다.
      - JuiceMaker: FruitStore 인스턴스에 접근 해, 주스 주문 및 과일 재고 수정을 하는 Struct 입니다.
      - JuiceMakerException: 주스 주문시 과일 개수가 없는 경우, 과일 재고가 0보다 작은 경우의 예외를 처리합니다.
      - JuiceType: 쥬스 종류를 정의합니다. 또한, 쥬스 종류에 따라 소모되는 과일과 개수를 정의합니다.
   - View

[목차로 돌아가기](#목차)
<br><br>

## 흐름도:ocean:
- **쥬스 선택**
```mermaid
sequenceDiagram
actor 손님
손님 ->> View: 쥬스 메뉴 선택
View ->> Controller: 어떤 메뉴 선택했는 지 전달
Controller ->> JuiceMaker: 선택된 쥬스의 재료 전달
loop 쥬스의 재료 과일의 수
  JuiceMaker ->> FruitStore: 과일의 수량 확인
  opt 과일의 수량이 부족하다면
    FruitStore ->> Controller: negativeCountError 던짐.
    Controller ->> View: 수량 부족 알림 전달
  end
end
loop 쥬스의 재료 과일의 수
  Note over FruitStore: 수량의 변화
end
Controller ->> FruitStore: 증가(감소)된 수량 확인
Controller ->> View: 수량 적용, 쥬스 제조 완료 알림 전달
```

- **과일 수량 증감**  <a name="section-2"></a>
```mermaid
sequenceDiagram
actor 사장님
사장님 ->> View: 수량 증가 or 감소 버튼 클릭
View ->> Controller: 과일 수량의 변화
alt 과일 수량이 감소했을 경우
  Controller ->> JuiceMaker: 수량 감소 요청
  JuiceMaker ->> FruitStore: 수량 감소 함수 실행
  opt 과일의 수량이 음수가 될 경우
    Note over FruitStore: 변화 없음
  end
else 과일 수량이 증가했을 경우
  Controller ->> JuiceMaker: 수량 증가 요청
  JuiceMaker ->> FruitStore: 수량 증가 함수 실행
end
Note over FruitStore: 수량의 변화
Controller ->> FruitStore: 증가(감소)된 수량 확인
Controller ->> View: 수량 적용
```

[목차로 돌아가기](#목차)
<br><br>

## 고민했던점 및 궁금했던점:interrobang:	

