## glowfi.sh v2 - Because the Zombie Apocalypse is coming

### Installation

Just grab a copy of one of the frameworks (either for the simulator or for release, the device).

```swift
import Glowfish

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
...
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	Glowfish.setCredentials("123", authSecret: "321")
```

### Changing the training set

There may be times throughout your application to group training sets that may not necessarily correspond to each other.

glowfi.sh has setup app sets specially for this purpose.

```swift
import Glowfish
...
Glowfish.appSet("set name")
```

### Defining Training

Training can be done in 2 different fashions and we'll need to know which ones your application uses.

**Product/Feature/Entity** - Used for returning products that are related to a user or users that are related to a product.

**Social** - Used for returning users related to another user.

```swift
import Glowfish

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
...
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	Glowfish.setCredentials("123", authSecret: "321")
	Glowfish.useObjects() // training for products/features/entities
	Glowfish.useSocial() // train for social
```

### The Objects

**GFUser** - The user object that acts on features/products/entities. Usually this corresponds directly with a device or the "logged in" user for an application.

**GFObject** - A convenience wrapper for any products, feature or entity other than a user. This is any object that can receive a rating from a GFUser.

**GFReference\<T: (Int|Float|Bool)>** - The object returned from creating a GFObject with additional reference material for type casting.

#### Creating The Objects

```swift
let user: GFUser = GFUser.create("String Id Of User")
let product: GFResource<NSInteger> = GFObject.create("String Id of Product")
```

#### Rating a product

```swift
let user: GFUser = GFUser.create("String Id Of User")
let product: GFResource<NSInteger> = GFObject.create("String Id of Product")

product.rate(user, rating: 4) {
	(result, error) -> Void in
	if error != nil {
		// something went wrong with training
	} else {
		// training successful
	}
}
```

#### Retrieving Predictions

```swift
let user: GFUser = GFUser.create("String Id Of User")
let maxResults: Int = 5
// Get objects given a single user
user.objectsForThis(5) {
	(objects, error) -> Void in
	if error != nil {
		// something went wrong with getting the predictions
	} else {
		println("Objects: \(objects)")
	}
}

// Get users given another user
user.usersForThis(maxResults) {
	(users, error) -> Void in
	if error != nil {
		// something went wrong with getting the predictions
	} else {
		println("Users: \(users)")
	}
}

// Get users given a single object
let product: GFResource<NSInteger> = GFObject.create("String Id of Product")
product.usersForThis(maxResults) {
	(users, error) -> Void in
	if error != nil {
		// something went wrong with getting the predictions
	} else {
		println("Users: \(users)")
	}
}
```
