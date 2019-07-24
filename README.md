# Goodoc Swift Style Guide

## Swift 4.x

### Goodoc iOS Developers의 코드 스타일을 지정하여 코드 분석에 유리하고 코드 가독성을 높여 개발 퍼포먼스를 향상시키기 위해 지정한 가이드입니다.

#### 변경사항은 점진적인 형태로 개선합니다.

#### 가이드는 권장사항과 *필수항목을 분류하며 반드시 지켜야할 규약은 `SwiftLint`로 관리합니다.

#### 참고
- [StyleShare](https://github.com/StyleShare/swift-style-guide/blob/master/README.md)
- [SwiftStyleGuide](https://google.github.io/swift/)

## 목차

[네이밍 규칙](#네이밍-규칙)

- [프로토콜](#프로토콜)
- [클래스](#클래스)
- [구조체](#구조체)
- [함수](#함수)
- [프로퍼티](#프로퍼티)
- [열거형](#열거형)
- [파일](#파일)

[코드 규칙](#코드-규칙)
- [임포트](#임포트)
- [태그](#태그)
- [주석](#주석)
- [코드라인](#코드라인)
- [프로토콜 확장](#프로토콜-확장)
## 네이밍 규칙

### 프로토콜
- 모든 프로토콜은 UpperCamelCase로 표기합니다.
- 프로토콜 이름 뒤에 Delegate, DataSource, Type 으로 표기합니다.

	<details>
	<summary>Sample</summary>

	``` swift
	protocol CommonCellDelegate {}
	protocol CommonTableViewDataSource {}
	```

	``` swift
	protocol CommonNetworkType {}
	protocol ViewModelType {}
	```
	</details>
	
### 클래스
- 모든 클래스는 UpperCamelCase로 표기합니다.

### 구조체
- 모든 구조체는 UpperCamelCase로 표기합니다.
- 모델의 경우 구조체의 이름은 되도록 명사로 표기하고 내부 구조를 Request, Response로 구분하며 Response의 경우 Mappable 채택하여 정의합니다.
- 구조체 내부에는 클래스를 정의하지 않습니다.
	<details>
	<summary>Sample</summary>

	``` swift
	struct Notice {

		struct Request {
			// ...
		}

		struct Response: Mappable {
			// ...
		}

		struct Detail {
			// ...
		}
	}
	```

	``` swift
	struct NoticeModel { X
		// ...
	}

	struct NoticeList { X
		// ...

		class NoticeViewModel { X
			// ...
		}
	}
	```
	</details>

### 함수
- 모든 함수는 lowerCamelCase로 표기합니다.
- 모든 함수 이름앞에 get을 적용하지 않습니다.

	<details>
	<summary>Sample</summary>

	``` swift
	func email() {
		// ...
	}
	```
	
	``` swift
	func getEmail() { X
		// ...
	}
	```
	</details>

### 프로퍼티
- 모든 프로퍼티는 lowerCamelCase로 표기합니다.
- 이름에 약어가 들어가는경우 앞에서 시작하면 소문자, 뒤에 들어가는경우 대문자로 입력합니다.

	<details>
	<summary>Sample</summary>

	``` swift
	var description: String?
	let noticeKey: String = "notice_seq"
	
	var html: String?
	var userID: String?
	```
	
	``` swift
	var Description: String?  X
	let KNoticeKey: String = "notice_seq"  X
	let NOTICE_SEQ: String = "notice_seq"  X

	var HTML: String?	X
	var userId: String?	X
	```
	</details>

### 열거형
- 모든 열거형은 UpperCamelCase로 표기합니다.
- 모든 열거형의 case는 lowerCamelCase로 표기합니다.
- 열거형 이름뒤에 Type, Code으로 표기합니다.

	<details>
	<summary>Sample</summary>

	``` swift
	enum NoticeType {
		case .event
		case .terms
	}
	
	enum StatusCode: String {
		case success = "0001"
	}
	```
	
	``` swift
	enum notice {  X
		case .Event  X
		case .terms
	}

	enum StatusCodeType: String {  X
		case success = "0001"
	}
	```
	</details>

### 파일
- 파일이름에 되도록 Common, Info, data등을 표기하지 않습니다.
	<details>
	<summary>Sample</summary>
	
	- Notice.swift O
	- NoticeInfo.swift X
	- NoticeData.swift X
	</details>

##코드 규칙


### 임포트
- 임포트는 알파벳 순서로 정렬합니다.
- 기본 프레임워크를 먼저 임포트하고 서드파티 프레임워크를 위에 공백 포함 임포트 합니다.
	<details>
	<summary>Sample</summary>
	``` swift
	import Foundation
	
	import Alamofire
	import ObjectMapper
	```
	</details>

### 태그
- 태그 메시지 앞에 `-` 를 추가합니다.
- 태그 메시지를 작성하는 라인의 위에 공백을 추가합니다.
	<details>
	<summary>Sample</summary>
	``` swift
	
	// MARK: - Properties
    var message: String = ""

	// MARK: - View Life cycle
    override func viewDidLoad() {
        super.viewDidLoad()
	}
	```

	``` swift
	// MARK: Properties	X
    var message: String = ""
	// MARK: - Request	X
	func loadNoticeList() {
		// ...
	}
	```
	</details>

### 주석
- swift 기본 표기법을 사용합니다. (`command` + `option` + `/`)
- 열거형의 주석은 case에 별도로 작성합니다.

	<details>
	<summary>Sample</summary>
	``` swift
	/// 공지사항 리스트를 불러오는 함수
	func loadNoticeList() {
		// ...
	}

	/// 공지사항 API 요청
	///
	/// - Parameter completion: 통신 결과를 나타내는 상태코드
	static func noticeList(_ completion: Network.Status)

	/// 공지사항 타입
	enum NoticeType {
		/// 이벤트
		case .event
		/// 이용약관
		case .terms
	}
	```

	``` swift
	/**
	  공지사항 리스트를 불러오는 함수	X
	*/
	func loadNoticeList() {
		// ...
	}

	/// 공지사항 타입
	///
	/// - event: 이벤트	X
	/// - terms: 이용약관	X
	enum NoticeType {
		case .event
		case .terms
	}
	```
	</details>

### 코드라인
- 작성하는 코드의 최대 라인 수는 `150`자 이하로 작성합니다.

### 프로토콜 확장
- 프로토콜을 채택하여 사용하는경우 extension으로 구분하여 작성합니다

	<details>
	<summary>Sample</summary>
	``` swift
	// MARK: - NoticeViewModelType
	extension NoticeViewModel: NoticeViewModelType {
		// ...
	}

	// MARK: - UITableViewDelegate
	extension NoticeViewController: UITableViewDelegate {
  	// ...
	}
	```

	``` swift
	class NoticeViewModel: NoticeViewModelType {	X
		// ...
	}

	class NoticeViewController: UIViewController, UITableViewDelegate {	X
		// ...
	}
	```
	</details>
