# Equatable

```swift
import UIKit


struct LoginInfo2: Codable {
    
    var authKey: String
    var usrNo: Int
    var usrNm: String?
    var crpNo: Int?
    var crpNm: String?
}

struct LoginInfo: Codable, Equatable {

    var authKey: String
    var usrNo: Int
    var usrNm: String?
    var crpNo: Int?
    var crpNm: String?

    static func == (lhs: LoginInfo, rhs: LoginInfo) -> Bool {
        return lhs.usrNo == rhs.usrNo
    }
}

func unique(infos2: [LoginInfo2]) -> [LoginInfo2] {

    var uniqueInfos2 = [LoginInfo2]()

    for info2 in infos2 {
        if !uniqueInfos2.contains(where: { info2 in
            
            print(info2)
            return info2.usrNo == 8392 ? false : true
        }) {
            uniqueInfos2.append(info2)
        }
    }

    return uniqueInfos2
}

func unique(infos: [LoginInfo]) -> [LoginInfo] {

    var uniqueInfos = [LoginInfo]()

    for info in infos {
        if !uniqueInfos.contains(info) {
            uniqueInfos.append(info)
        }
    }

    return uniqueInfos
}

var infos = [LoginInfo]()
var infos2 = [LoginInfo2]()
// Adding data models to data source

let info1 = LoginInfo(authKey: "1234567890", usrNo: 8392)
let info2 = LoginInfo(authKey: "abcdefgh", usrNo: 8392)
let info3 = LoginInfo(authKey: "ㄱㄴㄷㄹㅁㅂㅅ", usrNo: 8392)

let info4 = LoginInfo2(authKey: "1234567890", usrNo: 8392)
let info5 = LoginInfo2(authKey: "abcdefgh", usrNo: 8392)
let info6 = LoginInfo2(authKey: "ㄱㄴㄷㄹㅁㅂㅅ", usrNo: 8392)

infos.append(info1)
infos.append(info2)
infos.append(info3)

infos2.append(info4)
infos2.append(info5)
infos2.append(info6)

// Now contains only two elements.
let uniqueInfos = unique(infos: infos) // authKey: "1234567890", usrNo: 8392

let uniqueInfos2 = unique(infos2: infos2)
// authKey: "1234567890", usrNo: 8392
// authKey: "abcdefgh", usrNo: 8392
// authKey: "ㄱㄴㄷㄹㅁㅂㅅ", usrNo: 8392
```
