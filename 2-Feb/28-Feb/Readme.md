# UITableView with Searching capability

### Shout: Thanks to https://www.raywenderlich.com/4363809-uisearchcontroller-tutorial-getting-started#toc-anchor-001

## Main Interface 
<p align="center">
  <img src="./Images/Main Interface.png" width="400" height="400" title="Initial VC">
</p>

##### The application has threes cells with entries from the struct uith a function that generates sample data

### Struct Definition
```
import Foundation

struct SampleData {
    var sample: String
    var details: String
    
    func generateData() -> [SampleData] {
        [SampleData(sample: "Sample1", details: "This is sample one"),
         SampleData(sample: "Sample2", details: "This is sample two"),
         SampleData(sample: "Sample3", details: "This is sample three")
        ]
    }
}
```
##### ```func generateData()``` is used for geneerating the data 

## StoryBoard Configuration
<p align="center">
  <img src="./Images/StoryBoard.png" width="500" height="400" title="Initial VC">
</p>

- TableViewController embedded in Navigation Controller
- Navigation Controller is the Initial Controlller
- Inserted label in TableViewCell and details VC
- Added a button to dismiss the current view => details VC
- TableViewController has a custom class => SampleTableViewController
- TableViewCell has a custom class => SampleTableViewCell => NOTE: I don't even know I need it
- Details VC had a custom class => SampleDetailVC
- Segue Identifier from the tableView to details VC => showDetail
