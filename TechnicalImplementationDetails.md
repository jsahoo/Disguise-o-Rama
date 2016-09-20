# Disguise-o-Rama Coding Challenge

## Technical Implementation Details

### Launch Screen
Use LaunchScreen.storyboard to create the launch screen. Use Storyboards + AutoLayout to create the screen. Should consist of UILabels for the text and UIImages for the images.

### Animated Transition from Launch Screen to Main Screen
Using Storyboard + AutoLayout, create the Initial View Controller as a UIViewController. Create it so that it looks identical to LaunchScreen.storyboard. In code, use a UIView.animateWithDuration block to animate all of the elements off the screen and move Scotch into position.

Everything above the ring should be moved up and off the screen by changing the .center to a new CGPoint comprised of the same **x** value but a **y** value equal to _negative_ half of the element's height (this will ensure the element is completely off of the screen).

```
UIView.animate(withDuration: 0.5) {
            self.button.center = CGPoint(x: self.button.center.x, y: -self.button.bounds.height/2)
        }
```

Everything below the ring should be moved down and off the screen by changing the .center to a new CGPoint comprised of the same **x** value but a **y** value equal to the screen height + half of the element's height

```
UIView.animate(withDuration: 0.5) {
    self.button.center = CGPoint(x: self.button.center.x, y: UIScreen.main.bounds.height + self.button.bounds.height/2)
}
```

The ring will be animated off the screen by setting it's height and width such that both values are greater than the screen's bounds.

And finally we need to move Scotch into position by scaling his height and width proportionally to each other until the bottom of the image is aligned with the bottom of the screen.

### Intro Screen/Tutorial
We could build on top of the previous screen or create a new screen that looks just like the last configuration of the previous screen (with just Scotch zoomed into position on the white background). Either way, we need to add a UIButton, a UIImage for the text bubble line, and a UICollectionView consisting of UICollectionViewCells containing just a UILabel for the text. Each of these elements need to be animated into view in a similar manner to how the previous elements were animated out using `UIView.animate(withDuration:)`. The UICollectionView should be setup to display only one cell at a time. Clicking the "next" button advances the displayed cell to the next.

Once we've reached the end of intro, zoom out Scotch and animate out the UIButton and UICollectionView with `UIView.animate(withDuration:)`.

### Main Screen
The main screen is initiated with Scotch on a white background in the same "zoomed out" position that he was at on the previous screen just before transitioning to this screen. We'll animate the disguise bubbles into place from the center of the screen.

#### Download Additional Disguises
Next we need to handle the downloading of additional disguises. Since we're only dealing with one download, let's just use NSURLSession. If there were many network requests, I would consider using `Alamofire` instead. Let's also use `SwiftyJSON` to more easily work with the JSON that we get back.

#### Modeling the Data
Since caching is a requirement, let's create models for the data using classes rather than structs as we can easily archive classes (that conform to NSCoding) to disk with NSKeyedArchiver.

#### Displaying the disguises
As for actually displaying the disguises, we need a second UIImageView constrained with the same heigh, width, and bounds as the UIImageView containing Scotch. When a disguise is selected, we set the overlaid UIImageView to the disguise. When Scotch is tapped (to remove the disguise), set the overlaid UIImageView.image to nil.

#### Rotating Circular menu
I'm not entirely sure how to build this so I would need to do some research, most likely pertaining to UIKit Dynamics. Maybe follow a tutorial like [this one](https://www.raywenderlich.com/9864/how-to-create-a-rotating-wheel-control-with-uikit) from raywenderlich.com.

#### Falling Disguise bubbles
Again, not entirely sure how to build this functionality, so I would research UIKit Dynamics and follow a tutorial like [this](https://www.sitepoint.com/using-uikit-dynamics-swift-animate-apps/) or [this](https://www.raywenderlich.com/76147/uikit-dynamics-tutorial-swift)
