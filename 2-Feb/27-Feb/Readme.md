# Happy Day IOS app via Advanced IOS Volume 1

##### Initial View Controller: Navigation Controller in which the Happy Days CollectionView is embedded in

<p align="center">
  <img src="./Images/Initial VC.png" width="600" height="400" title="Initial VC">
</p>

##### But....inside viewDidAppear is the checkPermissions() function
```
 override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        checkPermissions()
    }
```
and by default..... ```let photosAuthorized = PHPhotoLibrary.authorizationStatus() == .authorized``` is ```false```

```
func checkPermissions() {
        // check status for all three permissions
        let photosAuthorized = PHPhotoLibrary.authorizationStatus()
            == .authorized      
        
        if photosAuthorized == false {          
            if let vc = storyboard?.instantiateViewController(withIdentifier: "FirstRun") {
                navigationController?.present(vc, animated: true)               
            }
        }
    }
```
the vc will show the ViewController that has the FirstRun identifier


<p align="center">
  <img src="./Images/FirstRun StoryBoard ID.png" width="600" height="400" title="StoryBoard ID">
</p>

```
 @IBAction func requestPermission(_ sender: Any) {
        requestPhotosPermissions()
    }
    .....
    
// I am pretty proud of the code below utilizing the requestAuthorization 
    func requestPhotosPermissions() {
        
        PHPhotoLibrary.requestAuthorization { (PHAuthorizationStatus) in
            DispatchQueue.main.async {
                if PHAuthorizationStatus == .authorized {
                    self.authorizationComplete()
                } else {
                    self.PermissionLabel.text = "Create a button to re-enable my app to ask for permissions again"
                }
            }
        }
    }
```
if ALLOW ACCESS TO ALL PHOTOS is selected = ```PHAuthorizationStatus == .authorized```   
NOTE: I am showing changing configurations on info.plist  


<p align="center">
  <img src="./Images/NSPhotoLibraryUsageDescription.png" width="300" height="600" title="Message from Info.plist">
  <img src="./Images/info.png" width="500" height="600" title="Info.plist">
</p>

dismisses the VC that was presented modally....GO to CollectionViewController

```
    func authorizationComplete() {
        dismiss(animated: true)
    }
```
And now we are at the collection view controller....keep in mind, I have not added any photos yet...

<p align="center">
  <img src="./Images/CollectionVC.png" width="300" height="400" title="StoryBoard ID">
</p>


### TO BE CONTINUED
