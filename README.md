## glowfi.sh v2 - Because the Zombie Apocalypse is coming

### Installation

Just grab a copy of one of the frameworks (either for the simulator or for release, the device).

```swift
import Glowfish

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
...
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	Glowfish.setCredentials(<token>, authSecret: <secret>)
```

### Changing the training set

Training sets are sets of user events recorded during mobile app sessions that glowfi.sh uses to make future recommendations. There may be times throughout your application to group training sets that may not necessarily correspond to each other (e.g., user networks).

glowfi.sh has created app sets specifically for this purpose.

```swift
import Glowfish
...
Glowfish.appSet("set name")
```

### Defining Training (data/user events sent to glowfi.sh to build recommendations)

Training can be done in 2 different fashions and we'll need to know which ones your application uses.

**Product/Feature/Entity** - Used for returning product recommendations that are related to a user or users that are related to a product.

**Social** - Used for returning recommendations of users related to another user.

```swift
import Glowfish

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
...
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	Glowfish.setCredentials(<token>, authSecret: <secret>)
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

#### Sending glowfi.sh user events (ratings, likes, etc.) for training 

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

#### Retrieving Recommendations for users or objects from glowfi.sh

```swift
let user: GFUser = GFUser.create("String Id Of User")
let maxResults: Int = 5
// Recommend objects given a single user
user.objectsForThis(5) {
	(objects, error) -> Void in
	if error != nil {
		// something went wrong with getting the predictions
	} else {
		println("Objects: \(objects)")
	}
}

// Recommend users given another user
user.usersForThis(maxResults) {
	(users, error) -> Void in
	if error != nil {
		// something went wrong with getting the predictions
	} else {
		println("Users: \(users)")
	}
}

// Recommend users given a single object
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
