### 2023.01.20
## collectionView header 설정

collectionView header 설정
  // TODO: 블로그 포스팅
  1. create UICollectionReusableView
  2. regist UICollectionReusableView on CollectionView
  3. set size UICollectionReusableView on Flowlayout  

# CompositionalLayout 에서 사용되는 방법

1. `UICollectionReusableView` 상속하는 `CustomView를` 만든다.
2. `CollectionView`에 regist 해준다
3. `UICollectionViewCompositionalLayout` 에서 config & layout 해준다
   
## Example

```swift
// 1. UICollectionReusableView 상속하는 CustomView를 만든다.

class SampleReusableView: UICollectionReusableView {

    static let identifier = String(describing: SampleReusableView.self)

    private let label: UILabel = {
        let label = UILabel()
        
        label.text = "인원정보"
        label.textAlignment = .left
        label.textColor = .color(.blackberry_34_34_34)
        label.font = .boldSystemFont(ofSize: 16)
        
        return label
    }()

    func configure() {

        backgroundColor = .white
        addSubview(label)

        NSLayoutConstraint.activate([
            label.topAnchor.constraint(equalTo: topAnchor, constant: 28),
            label.leadingAnchor.constraint(equalTo: leadingAnchor, constant: 32)

        ])

    }

    override func layoutSubviews() {

        super.layoutSubviews()

        label.frame = bounds
    }
}
..
..

// 2. CollectionView에 regist 해준다
collecionView.register(
	SampleReusableView.self,
	forSupplementaryViewOfKind: UICollectionView.elementKindSectionHeader,
	withReuseIdentifier: SampleReusableView.identifier
)
..
..

// 3. `UICollectionViewCompositionalLayout` 에서 config & layout 해준다
private func createLayout() -> UICollectionViewCompositionalLayout {

	return UICollectionViewCompositionalLayout { sectionNumber, env -> NSCollectionLayoutSection? in
	
		let headerSize = NSCollectionLayoutSize(
			widthDimension: .fractionalWidth(1.0),
			heightDimension: .absolute(68.0)
		)

		let headerSupplementary = NSCollectionLayoutBoundarySupplementaryItem(
			layoutSize: headerSize,
			elementKind: UICollectionView.elementKindSectionHeader,
			alignment: .top
		)

        let itemCount = employList.count == 0 ? 1 : employList.count

        let groupHeight: CGFloat = CGFloat(employList.count) * 56.0

        let itemSize = NSCollectionLayoutSize(
	        widthDimension: .fractionalWidth(1.0),
	        heightDimension: .fractionalHeight(1.0)
	    )

        let item = NSCollectionLayoutItem(layoutSize: itemSize)

        let groupSize = NSCollectionLayoutSize(
	        widthDimension: .fractionalWidth(1.0),
	        heightDimension: .absolute(groupHeight)
		)

        let group = NSCollectionLayoutGroup.vertical(
	        layoutSize: groupSize,
	        subitem: item,
	         count: itemCount
		)

        let section = NSCollectionLayoutSection(group: group)

        section.contentInsets = NSDirectionalEdgeInsets(
	        top: 0,
	        leading: 0,
	        bottom: 8,
	        trailing: 0
		)

        section.boundarySupplementaryItems = [headerSupplementary]

        return section
	}
}
```

