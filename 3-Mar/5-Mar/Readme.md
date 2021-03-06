# SwiftUI Frontend

## What it looks like?

<p align="center">
  <img src="./images/pcap search.png" width="500" height="800" title="SDK Setup">
</p>

### Software.swift => this defines the key: value pair of the json data
```
struct Software: Codable, Hashable {
    var AppName: String
    var FileName: String
    var Sha1: String
}
```

### AppDBHandler.swift => helper file tha pulled data from my mongodb 
```
class AppDBHandler: ObservableObject {
    
    @Published var myResponse = [Software]()
    
    init() {
        guard let url = URL(string: "http://localhost:5555/apps") else { return }
        URLSession.shared.dataTask(with: url) { (data, response, error) in
            guard let data = data else { return }
            let decodedResponse = try! JSONDecoder().decode([Software].self, from: data)
            DispatchQueue.main.async {
                self.myResponse = decodedResponse
            }
        }.resume()
    }
}
```
#### NOTE: What took me hours was I was stubborn not to implement the ```AppDBHandler: ObservableObject``` and ```@Published var myResponse = [Software]()```. Both declarations would allow me to utilize the class's data across multiple views.  

### Main app => I had to declare variables in the main app because the primary view (```ContentView()```) had parameters 
```
@main
struct appDBDemoApp: App {
    
    @State private var text = ""
    @ObservedObject private var software = AppDBHandler()
    
    var body: some Scene {

        WindowGroup {
            ContentView(text: $text, softwares: software)
        }
    }
}
```

### ContentView = primary view => Made me understand ```@Binding``` and ```@ObservedObject``` and how it was important to declare it to propogate in the project. 
@Binding goees back to source of truth and I think the contentview has the source of truth

```
 struct ContentView: View {
    
    // Use a binding to create a two-way connection between a property that stores data, and a view that displays and changes the data
    @Binding var text: String
    
    @ObservedObject var softwares = AppDBHandler()
    
    var body: some View {
        NavigationView {
            Form {
                VStack {
                    Text("Enter Search Term")
                    SeacrhBar(text: $text)
                }
                Section {
                    Text("Results").foregroundColor(.green)
                    ForEach(softwares.myResponse, id: \.self) { item in
                        if item.AppName.contains(text) || item.FileName.contains(text) ||
                            item.Sha1.contains(text)
                        {
                            ResultRow(result: item.AppName, software: item)
                            ResultRow(result: item.FileName, software: item)
                            ResultRow(result: item.Sha1, software: item)
                        }
                    }
                }
            }.navigationTitle("Pcap's App Search")
        }
    }
}
struct ContentView_Previews: PreviewProvider {
    
    @State static var appsName = AppDBHandler()
    
    static var previews: some View {
        ContentView(text: .constant(""), softwares: appsName)
    }
}
```

### Created a ResultRow => Created a seperate view for each row so I can utilize the navigattionLink to move to the ```DetailView```
```
struct ResultRow: View {
    
    var result: String
    
    var software: Software
    
    var body: some View {
        NavigationLink(destination: Details(software: software)) {
            Text(result)
        }
    }
}
struct ResultRow_Previews: PreviewProvider {
    
    static var result = String()
    
    static var software = Software(AppName: "", FileName: "", Sha1: "")
    
    static var previews: some View {
        ResultRow(result: "", software: software)
    }
}
```

### DetailView => This view taught me two things.....I gotten better with Previews and with Sections 
```
struct Details: View {
    
    var software: Software
    
    var body: some View {
        Form {
            Section(header: Text("Details")) {
                HStack {
                    Text("Appname:    ")
                    Text("\(software.AppName)")
                }
                HStack {
                    Text("Filename:    ")
                    Text("\(software.FileName)")
                }
                HStack {
                    Text("SHA-1:        ")
                    Text("\(software.Sha1)")
                }
                
            }
        }
       
    }
}

struct Details_Previews: PreviewProvider {
    
    static var software = Software(AppName: "Pcap", FileName: "Pcap.txt", Sha1: "random")
    
    static var previews: some View {
        Details(software: software)
    }
}
```

### SearchBar => I definitely copied pasted the search bar but understood definitely how it worked.   
If I click inside the textfield, the cancel button appears and multiply circle fill appears. If you click the cancel button, the texfield clears up.  
```isEditing``` is the key bool that enables all this

```
struct SeacrhBar: View {
    
    @Binding var text: String
    
    @State private var isEditing = false
        
    var body: some View {
        TextField("Search ...", text: $text)
            .autocapitalization(.none)
            .padding(7)
            .padding(.horizontal, 25)
            .background(Color(.systemGray6))
            .cornerRadius(8)
            .overlay(
                HStack {
                    Image(systemName: "magnifyingglass")
                        .foregroundColor(.gray)
                        .frame(minWidth: 0, maxWidth: .infinity, alignment: .leading)
                        .padding(.leading, 8)
                    
                    if isEditing {
                        Button(action: {
                            self.text = ""
                        }) {
                            Image(systemName: "multiply.circle.fill")
                                .foregroundColor(.gray)
                                .padding(.trailing, 8)
                        }
                    }
                }
            )
            .padding(.horizontal, 10)
            .onTapGesture {
                self.isEditing = true
            }
        
        if isEditing {
            Button(action: {
                self.isEditing = false
                self.text = ""
                
            }) {
                Text("Cancel")
            }
            .padding(.trailing, 10)
            .transition(.move(edge: .trailing))
            .animation(.default)
        }
    }
}


struct SeacrhBar_Previews: PreviewProvider {
    static var previews: some View {
        SeacrhBar(text: .constant(""))
    }
}

```


 
