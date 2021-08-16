# SimpleCollectionView  
## **[Context](https://developer.apple.com/documentation/uikit/views_and_controls/collection_views/implementing_modern_collection_views)**  
### Implementing Modern Collection Views
Bring compositional layouts to your app and simplify updating your user interface with diffable data sources.  

## Preview  
<img src="https://user-images.githubusercontent.com/47273077/129506158-41541783-0909-41e2-90de-4f2feaa17642.png" width="300" height="600">

## Sample Code  
### UICollectionViewCell  
**[NumberCell](https://github.com/YamamotoDesu/SimpleCollectionView/blob/main/CollectionView/NumberCell.swift)**
```swift  
import UIKit

class NumberCell: UICollectionViewCell {
    static let reuseIdentifier = String(describing: NumberCell.self)
    
    @IBOutlet weak var label: UILabel!
    
}

```  

### UICollectionViewDiffableDataSource  
**[dataSource](https://github.com/YamamotoDesu/SimpleCollectionView/blob/main/CollectionView/ViewController.swift)**
```swift  
    enum Section {
        case main
    }

    @IBOutlet weak var collectionView: UICollectionView!
    
    var dataSource: UICollectionViewDiffableDataSource<Section, Int>!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        configureDataSource()
    }
    
    func configureDataSource() {
        dataSource = UICollectionViewDiffableDataSource<Section, Int>(collectionView: self.collectionView, cellProvider: { (collectionView, indexPath, number) -> UICollectionViewCell? in
            
            guard let cell = collectionView.dequeueReusableCell(withReuseIdentifier: NumberCell.reuseIdentifier, for: indexPath) as? NumberCell else {
                fatalError("Cannot create new cell")
            }
            
            cell.label.text = number.description
            return cell
        })
        
        var initialSnapshot = NSDiffableDataSourceSnapshot<Section, Int>()
        initialSnapshot.appendSections([.main])
        initialSnapshot.appendItems(Array(1...100))
        
        dataSource.apply(initialSnapshot, animatingDifferences: false)
        
    }

```  

## **[Layouts](https://developer.apple.com/documentation/uikit/views_and_controls/collection_views/layouts)**  
[<img src="https://user-images.githubusercontent.com/47273077/129505382-e22ca111-bcd6-47a9-8677-4394ca68992c.png" width="350" height="600">]  

## Arrange your collection view content in a highly configurable layout  
#### NSCollectionLayoutGroup(set heightDimension as absolute)  
[<img src="https://user-images.githubusercontent.com/47273077/129507027-c02c900d-7d7a-4e43-8332-5ebfd506e4f8.png" width="350" height="600">]  
```swift  
    override func viewDidLoad() {
        super.viewDidLoad()
        collectionView.collectionViewLayout = configureLayout()
    }
    
    func configureLayout() -> UICollectionViewCompositionalLayout {
        let itemSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .fractionalHeight(1.0))
        let item = NSCollectionLayoutItem(layoutSize: itemSize)
        item.contentInsets = NSDirectionalEdgeInsets(top: 5.0, leading: 5.0, bottom: 5.0, trailing: 5.0)
        let groupSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .absolute(44.0))
        let group = NSCollectionLayoutGroup.horizontal(layoutSize: groupSize, subitems: [item])
        
        let selction = NSCollectionLayoutSection(group: group)
        return UICollectionViewCompositionalLayout(section: selction)
        
    }

```  

#### NSCollectionLayoutItem(set fractionalWidth as 0.2)   
[<img src="https://user-images.githubusercontent.com/47273077/129507490-76c5090b-9bc3-407f-a6c0-b1c1b48a9bd4.png" width="350" height="600">]   
```swift  
    func configureLayout() -> UICollectionViewCompositionalLayout {
        let itemSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(0.2), heightDimension: .fractionalHeight(1.0))
        let item = NSCollectionLayoutItem(layoutSize: itemSize)
        item.contentInsets = NSDirectionalEdgeInsets(top: 5.0, leading: 5.0, bottom: 5.0, trailing: 5.0)
        let groupSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .absolute(44.0))
        let group = NSCollectionLayoutGroup.horizontal(layoutSize: groupSize, subitems: [item])
        
        let selction = NSCollectionLayoutSection(group: group)
        return UICollectionViewCompositionalLayout(section: selction)
        
    }
```  

