# SwiftUI concepts => CodingKey, ObservableObject, Codable, Published, Encoder and Decoder

### ObservableObject, Published and ObservedObject
```
class Sample: ObservableObject {
      @Published var access = "pcap"
}
```
Per apple dcoumentation, "A type of object with a publisher that emits the changed value before the object has changed.    
By default an ObservableObject synthesizes an objectWillChange publisher that emits the changed value before  
any of its @Published properties changes". It is useful when implementing objects across classes


# Playing around with Codable protocol

## Strings, by default comply with Codable protocol
```
class Sample: Codable {
  var pcap = ""
}
```

## But, when adding a property wrapper @Published, it is now not compliant with Codable. Property wrappers basically changes the type of the property to add functionality. Therefore, it changes the type altogether. @Published property wrapper is not in compliant with Codable
```
class Sample: Codable {
  @Published var pcap = ""
}
```
## To fix this,let's first implement a enum that is a CodingKey. The cases in the enum represents the keys in the JSON 
```
enum CodingKey: CodingKeys {
  case pcap
}
class Sample: Codable {
  @Published var pcap = ""
 
}
```
## Then, we can add encoding function 
```
enum CodingKey: CodingKeys {
  case pcap
}
class Sample: Codable {
  @Published var pcap = ""
 
   func encode(to encoder: Encoder) throws {
  
      // 1 KeyedEncodingContainer => This is like a dictionary you can store your properties in as you encode them. 
      var container = encoder.container(keyedBy: CodingKeys.self)
      
      // 2 Encode the name and id properties directly to the container
      try container.encode(pcap, forKey: .pcap)
  }
}
```

## Third, add decode function
```
enum CodingKeys: CodingKey {
  case pcap
}

class Sample: Codable {
  @Published var pcap = ""
    
    required init(from decoder: Decoder) throws {
    
        // 1 Get a keyed container from the decoder, this will contain all of the properties in the JSON
        let container = try decoder.container(keyedBy: CodingKeys.self)
        
        // 2 Extract the pcap value from the container using the appropriate type and coding key.
        pcap = try container.decode(String.self, forKey: .pcap)
     }
        
   func encode(to encoder: Encoder) throws {
  
      // 1 KeyedEncodingContainer => This is like a dictionary you can store your properties in as you encode them. 
      var container = encoder.container(keyedBy: CodingKeys.self)
      
      // 2 Encode the name and id properties directly to the container
      try container.encode(pcap, forKey: .pcap)
  }
}
```



