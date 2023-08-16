<details>
  <summary> 2022.11.02 - Push를 통한 화면전환 구조 변경 간 발생한 SideEffect </summary>
  AS-IS 푸시가 없었음, 그래서 푸시로 인한 화면 전환 로직이 없음
  ParentsViewController -> MainNavi -> MainViewController의 형태였음
  ParentsViewController -> NotiViewController로의 이동 간 VC <-> UINavigationController 전환이 어려운 상황

  TO-BE 

  [new]ParentsNavi -> ParentsViewController -> MainNavi -> MainViewController의 형태로 변경 -> 푸시 화면 전환 성공

  - Side Effect 발생

  -> MainViewController에서 SideMenu가 import 된 MenuViewController를 performSegue로 호출을 할 때 MainViewController가 사라짐

  - 원인

  ***여기서 seugue의 종류가 show로 되어있었음 -> present로 수정

  UIViewController에서는 화면 전환을 present, dismiss 호출하여 사용가능하며, UINavigationController의 화면 전환 메소드는 사용할 수 없다

  UINavigationController에서는 화면 전환을 push, pop 호출하여 사용가능하며, UIViewController의 화면 전환 메소드는 사용할 수 없다

  - 해결

  show의 특성은 호출하는 클래스에 맞춰서 화면 전환을 해준다.호출하는 화면의 클래스가 UINavigationController였기 때문에 SideMenu View를 push 해줬기에 Side Effect가 발생하였다
  segue를 끊고 화면 전환 코드를 작성해도 되었지만, 기존 코드를 살려 segue의 종류를 show -> present Modally 변경해주었다
</details>

<details>
  <summary> 2022.11.08 Xcode 14 cocoapods pod init이 되지않은 경우</summary>

  [블로그 포스팅 대체](https://plcprogrammer-dy.tistory.com/78)
</details>

<details>
  <summary> 2022.11.16 Xcode 14 No such module 'RxSwift', could not find module for target </summary>

  [블로그 포스팅 대체](https://plcprogrammer-dy.tistory.com/81)
</details>

<details>
  <summary> 2022.12.15 UICollectionView Dynamic Section height </summary>
  
  기존 UICollectionViewDelegateFlowLayout 을 채택하지않고 UICollectionView Compositional Layout를 사용하면서 생긴 일..
  
  3개의 섹션으로 구성되어있으며, 1번째 섹션을 제외하고 2, 3번째 섹션은 존재할 수도, 존재하지않을수도 있다.
  1번째 섹션 또한 UI Components 구성이 동적이다.
  
  1번째 섹션의 UI Component가 변하게 되어 1번째 섹션의 height가 줄어들어야했지만, 동적 처리 작업을 하지않았다.
  
</details>

<details>
  <summary> 2022.12.16 url->Data main thread warning </summary>
  
  Synchronous URL loading of 'url' should not occur on this application's main thread as it may lead to UI  unresponsiveness. 
  
  Please switch to an asynchronous networking API such as URLSession.
  
  Xcode 14로 변경되면서 thread warning이 표출되었다.
  
  url을 통해 UIImage(data: Data)로 init 하는 상황
 
 
  기존코드
  
  ```swift
  guard let url = URL(string: item.photo.url),
        let data = try? try? Data(contentsOf: url) else { return cell }
        
  DispatchQueue.main.async {
      convertedCell.bannerImage.image = UIImage(data: data)
  }
  ```
  
  대용량의 Data의 경우 main thread에서 작업 시 병목현상이 생길 수 있기 때문
  변경 후
  
  ```swift
  guard let url = URL(string: item.photo.url) else { return cell }
            
  URLSession.shared.dataTask(with: url) { data, response, error in
      guard let imageData = data else { return }
            
      DispatchQueue.main.async {
           convertedCell.bannerImage.image = UIImage(data: imageData)
      }
  }.resume()
  ```
  
</details>

<details>
  <summary> 2022.12.27 message sent to deallocated instance (property usage issue) </summary>
</details>

<details>
  <summary> 2023.01.06 협업 간 cocoapods 관리 문제 </summary>
  Podfile, Podfile.lock, Pods/
</details>

<details>
  <summary> 2023.01.12 CLLocationManager 이슈 </summary>
  Podfile, Podfile.lock, Pods/
</details>
  
 <details>
  <summary> 2023.01.12 Change background color of View inside TabView having NavigationView and ScrollView in SwiftUI </summary>
  [해답](https://stackoverflow.com/questions/70276467/tabview-background-transparency-doesnt-work-as-expected-with-scrollview-inside)
</details>
