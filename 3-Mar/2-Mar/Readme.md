# Searching with UISearchController

```let searchController = UISearchController(searchResultsController: nil)```
- The view controller that displays the search results. Specify nil if you want to display 
the search results in the same view controller that displays your searchable content

```var isSearchBarEmpty: Bool {
      return searchController.searchBar.text?.isEmpty ?? true
    }
```
- Nil-Coalescing Operator  
- isSearchBarEmpty will return true under two conditions / if the searchBar is empty and the default value true OR if ```searchController.searchBar.text?.isEmpty``` is nil

``` searchController.searchResultsUpdater = self```
- ```weak var searchResultsUpdater: UISearchResultsUpdating? { get set }``` => weak reference is just a pointer to an object that doesn't protect the object from being deallocated by ARC
- The object responsible for updating the contents of the search results controller

```searchController.obscuresBackgroundDuringPresentation = false```
- A Boolean indicating whether the underlying content is obscured during a search
- if you use the same view controller to display the searchable content and search results, it is recommended that you set this property to false

```navigationItem.searchController = searchController```
- The search controller to integrate into your navigation interface

```definesPresentationContext = true```
- A Boolean value that indicates whether this view controller's view is covered when the view controller or one of its descendants presents a view controller

```
extension SampleTableViewController: UISearchResultsUpdating {
  func updateSearchResults(for searchController: UISearchController) {
    
    let searchBar = searchController.searchBar
    filterContentForSearchText(searchBar.text!)
  }
}
```
- ```UISearchResultsUpdating``` A set of methods that let you update search results based on information the user enters into the search bar 
- ```searchController.searchResultsUpdater = self``` -> this complies with the UISearchResultsUpdating? protocol
- Test: If I delete the extension above, ```searchController.searchResultsUpdater = self``` will produce an error and will ask to add ```UISearchResultsUpdating``` as protocol the viewcontroller needs to conform with
