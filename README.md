<p align="center">
  <img max-width="500" style="object-fit: contain; width: 100%;" src="https://github.com/nerdsupremacist/Snap/blob/develop/Images/logo.png?raw=true">
</p>

# Snap

A customizable Snapping Drawer à la Apple Maps, Apple Music, Stocks, Overcast, etc.. 100% in SwiftUI 

This is heavily inspired by [Rideau](https://github.com/muukii/Rideau) and based on this [Gist](https://gist.github.com/mshafer/7e05d0a120810a9eb49d3589ce1f6f40) by [mshafer](https://github.com/mshafer).

Here's a short demo where I reconstructed the Apple Maps UI:

<img height="450" src="https://github.com/nerdsupremacist/Snap/blob/develop/Images/demo.gif?raw=true">

## Installation
### Swift Package Manager

You can install Snap via [Swift Package Manager](https://swift.org/package-manager/) by adding the following line to your `Package.swift`:

```swift
import PackageDescription

let package = Package(
    [...]
    dependencies: [
        .package(url: "https://github.com/nerdsupremacist/Snap.git", from: "0.1.0")
    ]
)
```

## Usage

Snap allows you to set up either 1, 2 or 3 Snapping points and customize your UI depending on where you are.

For example if we want to recreate the Apple Maps UI we could write the following:

```swift
import MapKit
import Snap
import SwiftUI

struct ContentView: View {
    @State private var region = MKCoordinateRegion(...)

    var body: some View {
        ZStack {
            Map(coordinateRegion: $region)

            SnapDrawer(large: .paddingToTop(24), medium: .fraction(0.4), tiny: .height(100), allowInvisible: false) { state in
                VStack(alignment: .leading, spacing: 10) {
                    SearchBar()

                    if state != .tiny {
                        Favorites()
                            .transition(.scale)
                    }

                    if state == .large {
                        Recents()
                            .transition(.scale)
                    }
                }
            }
        }
    }
}
```

Feel free to explore the API yourself and play around with it.

Other features include:
- Listening to state changes via a `@Binding`
- Setting a background view

## Contributions
Contributions are welcome and encouraged!

## License
Snap is available under the MIT license. See the LICENSE file for more info.

## Documentation (csd fork)

The blur effect can be changed in BlurView.swift by modifying lines 9 & 26

Possible style are:
let listBlurView: [BlurView] = [
        BlurView(style: .systemThickMaterial),              //0
        BlurView(style: .systemChromeMaterialLight),        //1
        BlurView(style: .systemChromeMaterial),             //2
        BlurView(style: .extraLight),                       //3
        BlurView(style: .systemMaterial),                   //4
        BlurView(style: .systemMaterialLight),              //5
        BlurView(style: .prominent),                        //6
        BlurView(style: .systemThinMaterialLight),          //7
        BlurView(style: .systemThinMaterial),               //8
        BlurView(style: .regular),                          //9
        BlurView(style: .regular),                          //10
        BlurView(style: .light),                            //11
        BlurView(style: .systemUltraThinMaterialLight),     //12
        BlurView(style: .systemUltraThinMaterial),          //13
        BlurView(style: .systemUltraThinMaterialDark),      //14
        BlurView(style: .systemThinMaterialDark),           //15
        BlurView(style: .systemChromeMaterialDark),         //16
        BlurView(style: .systemMaterialDark),               //17
        BlurView(style: .dark),                             //18
        BlurView(style: .systemThickMaterialDark),          //19
    ]

Examples of the effect of these can be seen [here:](https://gstvdfnbch.medium.com/two-ways-to-do-glassmophisms-in-swiftui-swiftui-uikit-uiblureffect-7b63da1a9292)
