DRKonamiCode
============

![](http://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Konami_Code.svg/300px-Konami_Code.svg.png)

[Konami code](http://en.wikipedia.org/wiki/Konami_Code) gesture recognizer for iOS. The recognizer is a subclass of UIGestureRecognizer has can be used in the same way as any other recognizer. Swipe gestures correspond to the Up/Down/Left/Right parts of the sequence. An optional feature allows you to implement a custom A+B+Enter action.

![](http://grab.by/fbga)

### Adding Konami Code to your Project ###

1. Drag DRKonamiGestureRecognizer.h and DRKonamiGestureRecognizer.m into your project
2. Add the gesture recognizer to one of your views using the following code.

```objective-c
_konamiGestureRecognizer = [[DRKonamiGestureRecognizer alloc] initWithTarget:self action:@selector(_konamiGestureRecognized:)];
[self.view addGestureRecognizer:self.konamiGestureRecognizer];
```

### A+B+Unlock ###

Optionally, you can require the user to enter A+B+Enter in order for the gesture to be recognized. You will need to implement the DRKonamiGestureProtocol which has required methods that let your UI respond to the request for the A, B, or Enter action. If you are not using the A+B+Enter feature than you do not need to set the recognizer's delegate.


```objective-c
_konamiGestureRecognizer = [[DRKonamiGestureRecognizer alloc] initWithTarget:self action:@selector(_konamiGestureRecognized:)];
[self.konamiGestureRecognizer setKonamiDelegate:self];
[self.konamiGestureRecognizer setRequiresABEnterToUnlock:YES];
[self.view addGestureRecognizer:self.konamiGestureRecognizer];

#pragma mark -
#pragma mark DRKonamiRecognizerDelegate

- (void)DRKonamiGestureRecognizerNeedsABEnterSequence:(DRKonamiGestureRecognizer*)gesture
{
	/// your code here. 
}

- (void)DRKonamiGestureRecognizer:(DRKonamiGestureRecognizer*)gesture didFinishNeedingABEnterSequenceWithError:(BOOL)error
{
	/// your code here.
}
```

### DRKonamiGestureProtocol ###

The DRKonamiGestureProtocol protocol is required only if you are using the A+B+Enter feature. The recognizer will inform its delegate when the A+B+Enter sequence is needed and when the sequence is no longer needed (due to gesture failing or succeeding).