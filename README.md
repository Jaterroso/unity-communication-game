# unity-communication-game
Simple tech demo about Unity WebGL build init and HTTPRequests


## Goal

The goal of this project is to provide a barebones example on how to init a webGL build and also how to communicate with someone who is using REST.

The game contains no 2D/3D assets, to keep it simple and to not violate copyrights.

## Initialization

The html calls the unity loader script.
After the loader finishes you have the opportunity to call the C# code (which was transpiled by emscripten).

For example imagine:
* there is a GameObject named 'Foo'.
* it has a ScriptComponent Bar.cs
* Bar.cs defines a Bar class which extends MonoBehavior
* Bar class has an instance method called 'SetValue' which accepts a string and returns void

To call this you can do the following in the js inside the html body.
``` javascript
script.onload = () => {
        createUnityInstance(canvas, config, (progress) => {
          progressBarFull.style.width = 100 * progress + "%";
        }).then((unityInstance) => {
          loadingBar.style.display = "none";
          // Start of Custom Code 
          unityInstance.SendMessage('Foo','SetValue','Hello world!');
          // End of Custom Code
          fullscreenButton.onclick = () => {
            unityInstance.SetFullscreen(1);
          };
        }).catch((message) => {
          alert(message);
        });
      };
```

You can also supply your own html template for the Unity WebGL build process, but I wanted to keep it simple.

## HTTPRequests

Unity has builtin support for HTTPRequests.
You can find a pretty dumbed down usage example in [](https://github.com/rkeeves/unity-communication-game/blob/main/Assets/CustomConfiguration.cs)

## Web build

You can find the web build in the webassembly-build directory of this repo.