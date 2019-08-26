#  Text Reader

This app demonstrates ...

Based on tutorial [Working with URL Schemes in iOS Apps](https://www.appcoda.com/working-url-schemes-ios/) by [Simon Ng](https://www.appcoda.com/author/admin/) of Appcoda.

The description of this app starts at the subtitle **Creating Your Custom URL Scheme**, after the discussion of previously introduced app **QRCode Reader**.

Set Bundle Identifier: `com.share-telematics.TextReader`

Edit `Info.plist` - add items:
```
Info.plist
  URLTypes
    URLIdentifier: com.share-telematics.TextReader
    URLSchemes:    textreader  
```
_Now the app accepts the URL in the form of textreader://<message>. 
We still need to write a few lines of code such that it knows what to do when another app launches the custom URL (e.g. textreader://Hello!)._

```
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {

  let message = url.host?.removingPercentEncoding
  let alertController = UIAlertController(title: "Incoming Message", message: message, preferredStyle: .alert)
  let okAction = UIAlertAction(title: "OK", style: UIAlertAction.Style.default, handler: nil)
  alertController.addAction(okAction)

  window?.rootViewController?.present(alertController, animated: true, completion: nil)

  return true
}
```

Build and run on iOS device or in simulator.

_You can open mobile Safari and enter `textreader://Great!%20It%20works!` in the address bar – you’ll be prompted to open the TextReader app. Once confirmed, the system should redirect you to the **TextReader** app and displays the Great! It works! message._

This works.

_Alternatively, you can use the **QRReaderDemo** app for testing. If you open the app and point the camera to the QR code shown below, the app should be able to decode the message but fails to open the TextReader app._

_You have to register the custom URL schemes before the method returns true. To register a custom scheme, open Info.plist of the **QRReaderDemo** project and add a new key named LSApplicationQueriesSchemes. Set the type to Array and add the following items:
(see the last few paragraphs in the [tutorial](https://www.appcoda.com/working-url-schemes-ios/))_



