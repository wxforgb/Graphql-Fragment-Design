# Graphql-Fragment-Design

If you use [graphql](https://graphql.org/) as your service's api server, you can try use the following methods to design your fragment.

## Design - 1

### base Fragment
```graphql
fragment BrandSimple on Brand {
    id
    name
    nameJaKana
}

fragment BrandImagePath on Brand {
    imagePath
}

fragment BrandItemCount on Brand {
    itemConnection {
        totalCount
    }
}

fragment BrandReviewCount on Brand {
    reviewConnection {
        totalCount
    }
}
```
![Design Example 1-1](Design-1-1.png)
```graphql
fragment BrandListSimpleView on Brand {
    ...BrandSimple
    ...BrandItemCount
}
```

![Design Example 1-3](Design-1-3.png)
```graphql
fragment BrandListView on Brand {
    ...BrandSimple
    ...BrandImagePath
    ...BrandReviewCount
}
```

![Design Example 1-2](Design-1-2.png)
```graphql
fragment BrandListView on Brand {
    ...BrandSimple
    ...BrandImagePath
    ...BrandItemCount
    ...BrandReviewCount
}

```

### Usage

```swift
extension BrandSimple {
}

extension BrandImagePath {
    var imageUrl: URL? {
        if let imagePath = imagePath, let imageUrl = URL(imagePath: imagePath) {
            return imageUrl
        }
        return nil
    }
}


extension BrandItemCount {
    var itemCount: Int {
        return itemConnection.totalCount
    }
}

extension BrandReviewCount {
    var reviewCount: Int {
        return reviewConnection?.totalCount ?? 0
    }
}
```
