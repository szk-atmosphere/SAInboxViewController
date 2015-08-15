# SAInboxViewController

[![Platform](http://img.shields.io/badge/platform-ios-blue.svg?style=flat
)](https://developer.apple.com/iphone/index.action)
[![Language](http://img.shields.io/badge/language-swift-brightgreen.svg?style=flat
)](https://developer.apple.com/swift)
[![Version](https://img.shields.io/cocoapods/v/SAInboxViewController.svg?style=flat)](http://cocoapods.org/pods/SAInboxViewController)
[![License](https://img.shields.io/cocoapods/l/SAInboxViewController.svg?style=flat)](http://cocoapods.org/pods/SAInboxViewController)

![](./SampleImage/sample.gif)

SAInboxViewController realizes Inbox like view transitioning.

## Features

- [x] Inbox like view transitioning
- [x] Scrolling up to begining of contents transitioning
- [x] Scrolling down to end of contents transitioning
- [x] Hedear dragging transitioning
- [x] Left edge swiping transitioning

## Installation

#### CocoaPods

SAHistoryNavigationViewController is available through [CocoaPods](http://cocoapods.org). If you have cocoapods 0.36.1 or greater, you can install
it, simply add the following line to your Podfile:

	pod "SAInboxViewController"


#### Manually

Add the [SAInboxViewController](./SAInboxViewController) directory to your project.

## Usage

If you install from cocoapods, you have to write `import SAInboxViewController`.

First of all, please use `SAInboxViewController` with `UINavigationController`.

There are two ViewControllers to realize Inbox transitioning. Please extend those ViewControllers.

1. `SAInboxViewController`... using as rootViewController
2. `SAInboxDetailViewController`... using as second ViewController

Those ViewControllers have `UITableView`, so implement ordinary `UITableView` behavior with that tableView.

If you use `UITableViewDelegate` in ViewController which extends `SAInboxDetailViewController`, please call super methods for below two methods.

```swift
override func scrollViewDidEndDragging(scrollView: UIScrollView, willDecelerate decelerate: Bool) {
    super.scrollViewDidEndDragging(scrollView, willDecelerate: decelerate)
}

override func scrollViewDidScroll(scrollView: UIScrollView) {
	super.scrollViewDidScroll(scrollView)
}
```

If you want to present ViewController from rootViewController, implement `func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath)` like this.

```swift
func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath) {
    let viewController = SAInboxDetailViewController()
    if let cell = tableView.cellForRowAtIndexPath(indexPath), cells = tableView.visibleCells() as? [UITableViewCell] {
        SAInboxAnimatedTransitioningController.sharedInstance().configureCotainerView(view, cell: cell, cells: cells, headerImage: headerView.screenshotImage())
    }        
    navigationController?.pushViewController(viewController, animated: true)
}
```

Implement `UINavigationControllerDelegate` methods, like this.

```swift
func navigationController(navigationController: UINavigationController, animationControllerForOperation operation: UINavigationControllerOperation, fromViewController fromVC: UIViewController, toViewController toVC: UIViewController) -> UIViewControllerAnimatedTransitioning? {
    return SAInboxAnimatedTransitioningController.sharedInstance().setOperation(operation)
}
```

## Requirements

- Xcode 6.4 or greater
- iOS7.0(manually only) or greater

## Author

Taiki Suzuki, s1180183@gmail.com

## License

SAInboxViewController is available under the MIT license. See the LICENSE file for more info.
