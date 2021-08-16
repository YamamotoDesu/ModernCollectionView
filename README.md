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
Arrange your collection view content in a highly configurable layout.  
[<img src="https://user-images.githubusercontent.com/47273077/129505382-e22ca111-bcd6-47a9-8677-4394ca68992c.png" width="350" height="600">]

![image](https://user-images.githubusercontent.com/47273077/129506031-de2cf9db-a607-426f-b943-a9c119821981.png)



