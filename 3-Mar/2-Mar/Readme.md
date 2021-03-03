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

