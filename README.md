# Project 2 - BeReal Part 1

Submitted by: Jeffrey Berdeal

BeReal Part 1 is an app that I attempted to replicate that can be used to share photos in real time with friends.

Time spent: 72 hours spent in total

## Required Features

The following **required** functionality is completed:

- [X] Users see an app icon in the home screen and a styled launch screen.
- [X] User can register a new account
- [X] User can log in with newly created account
- [X] App has a feed of posts when user logs in
- [X] User can upload a new post which takes in a picture from photo library and an optional caption	
- [X] User is able to logout	
 
The following **optional** features are implemented:

- [X] Users can pull to refresh their feed and see a loading indicator
- [X] Users can infinite-scroll in their feed to see past the 10 most recent photos
- [ ] Users can see location and time of photo upload in the feed	
- [X] User stays logged in when app is closed and open again	


The following **additional** features are implemented:

- [ ] List anything else that you can get done to improve the app functionality!

## Video Walkthrough

<div>
    <a href="https://www.loom.com/share/ea91c13957a44d32893eda942eb20795">
    </a>
    <a href="https://www.loom.com/share/ea91c13957a44d32893eda942eb20795">
      <img style="max-width:300px;" src="https://cdn.loom.com/sessions/thumbnails/ea91c13957a44d32893eda942eb20795-4f8162ca2d261757-full-play.gif">
    </a>
  </div>


## Notes

- Setting up ParseSwift with Back4App required careful alignment of the Swift models (AppUser, Post) with the server schema. Small mismatches (like objectId, createdAt, or GeoPoint types) caused decoding errors and broke the feed.
- Implementing login and signup was tricky because invalid session tokens (error 209) often appeared if a user logged out or the session expired. I had to learn how to properly reset AppUser.current and redirect to the login screen.
- Xcode repeatedly flagged “does not conform to ParseObject/ParseUser” until I discovered that ParseSwift requires a zero-argument initializer (init()) and sometimes originalData to satisfy protocol requirements.
- Infinite scroll (maybeLoadMore) and pull-to-refresh required async/await code. Debugging “Cannot find X in scope” errors taught me that all @State properties and helper functions had to live inside the FeedView struct.
- Early versions of PostRow crashed because of force-unwrapping post.image!.url or running async geocode tasks after a row was deallocated. Fixing this involved optional chaining and canceling geocoder tasks on disappear.
- Using .scaledToFill() with .aspectRatio(1, .fit) cropped/zoomed every image. Switching to .scaledToFit() fixed the issue and preserved full photos.
- Creating a dark theme with a custom header, avatar circles, relative timestamps, and location display required careful use of SwiftUI modifiers like .preferredColorScheme(.dark) and .scrollContentBackground(.hidden).
- Adding a custom logo required preparing a 1024×1024 PNG and configuring Assets.xcassets with the AppIcon set, something that wasn’t obvious at first.

## License

    Copyright 2025 Jeffrey Berdeal

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
