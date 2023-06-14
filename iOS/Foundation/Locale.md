
# 현재 로케일을 얻는 법

```swift
let currentLocale: Locale = Locale.current
let identifier: String = currentLocale.identifier
```

# Locale이 현재 지역과 다르게 나오는 경우

## How does iOS determine the language for my app?

A: To determine the language for your app, iOS considers not only the order of the user language preferences (in `General` > `Language` `&` `Region` of the `Settings` application) but also the localizations your app declares it supports. Here is the detailed process:

1.  1.  iOS는 먼저 사용자의 언어 기본 설정의 첫 번째 항목인 most preferred language를 찾습니다.
    
2. 앱에서 해당 언어를 지원하는지 확인합니다.  iOS는 preferred language와 일치하는 `.lproj`폴더 에 대한 앱 번들을 검색합니다 .  `.lproj` 폴더가 있으면 iOS는 앱이 해당 언어로 현지화되었다고 추론하고 앱에 대해 선택합니다. 그렇지 않으면 iOS는 사용자 언어 기본 설정에서 다음 언어를 선택한 다음 위의 확인을 반복합니다.
    
    The dialect support in iOS may slightly change the above behavior. If your user's preferred language is a regional variant that is not supported by your app, iOS will try to fall back to a more generic language before giving up. For example, if your user's preferred language is British English and your app bundle doesn't contain an `en-GB.lproj` or `en_GB.lproj` folder, iOS then searches your bundle for an `en.lproj` folder and chooses English for your app if the folder exists.
    
    **Note:** An `.lproj` folder is a directory that stores language-specific resources. See [Localized Resources in Bundles](https://developer.apple.com/library/ios/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html#//apple_ref/doc/uid/10000123i-CH101-SW7) and [Language and Locale IDs](https://developer.apple.com/library/ios/documentation/MacOSX/Conceptual/BPInternational/LanguageandLocaleIDs/LanguageandLocaleIDs.html#//apple_ref/doc/uid/10000171i-CH15-SW1) for details.
    
3.  앱에서 사용자의 기본 언어를 지원하지 않는 경우 iOS는 앱의 개발 지역과 일치하는 언어를 선택합니다 ([CFBundleDevelopmentRegion](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/TP40009249-130430-BAJJHDJH)).
    
    **Note:** 앱에 대해  `CFBundleDevelopmentRegion` 설정해야 합니다.
    기본 현지화를 채택하는 경우,  `CFBundleDevelopmentRegion` 의 값이 `Base.lproj` 폴더 콘텐츠에서 사용하는 언어와 일치하는지 확인하십시오.
    

시스템에서 앱의 언어를 선택하면, 일치하는 `.lproj` 폴더를 사용하여 localized resources를 찾습니다.
앱의 UI 또는 시스템 제공 UI 구성 요소 (text editing menus, UIDatePicker, UIImagePickerController and UILocalizedIndexedCollation) 가 잘못된 언어로 표시되는 경우 앱에 지원되는 모든 언어의 폴더가 포함되어 있고 `.lproj` 폴더의 이름이 올바른지 확인하세요.

앱이 `.lproj`폴더를 사용하지 않고 현지화된 리소스를 관리하는 경우 [CFBundleLocalizations](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-109552)을 사용하여 지원되는 언어를 지정해야 합니다

**Important:** The value of the Languages field in the App Store (under the Information section of your app) is determined by the existence of `.lproj` folders in your app bundle rather than by your app configuration in iTunes Connect. If you see the Languages field of your app doesn't contain exactly your supported languages, check if your app bundle contains the appropriate `.lproj` folders. If your app doesn't use `.lproj` folders to manage localized resources, make sure your app's `CFBundleLocalizations` specifies all your supported languages.

  

---
위와 같은 코드를 사용했지만 현재 프로젝트에서 en_KR 즉, 미국이 나온다


[참고링크](https://developer.apple.com/library/archive/qa/qa1828/_index.html)