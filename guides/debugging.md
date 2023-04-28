Did you ever see yourself placing `ShowDebug` everywhere in the code with comments like `Been here`, `If ok` and etc, just for trying to understand why your new groundbreaking feature isn't working correctly? The solution is called breakpoints.

## What is debugging?
Simply put, debugging is the ability to put breakpoints in your code and when the server will take that given path, it will pause the rest of the execution, and once it's paused you can inspect variables values, evaluate expressions directly on the `Immediate Window` and so on.

## Video

For the visual learners, I've recorded this video. It's using VS2019 but should work with any version.

[![Watch the video](https://img.youtube.com/vi/zz_LhL3hO0E/maxresdefault.jpg)](https://youtu.be/zz_LhL3hO0E)

## Setup

1. Once you have your solution opened with Visual Studio, open up the Solution Explorer and look for a folder called `server-components`.
2. Then you right click the `map-server` and select `Set as Startup Project`.
3. Next you will need to right click the `map-server` once again and this time open the `Properties` window.
4. On the left menu, select `Debugging`. Then on the right side panel, under `Work Directory`, change to `$(SolutionDir)`
5. Hit apply, then Ok.
6. Compile the solution.
7. Now you should be able to start _separately_ your `login-server` and `char-server`.
8. Once these are up, go back to Visual Studio and click the Play button at the top or hit F5 on the keyboard.
9. Go to any function in the `map-server` source code and put a breakpoint on any line and trigger that line on the client.
10. Your client should be frozen, the Visual Studio window should have taken the focus and you should see the line you selected hightlighted. You can now inspect variables, go forward with F10, release with F5, and so on.

## Tracing code path
Many times we need to know how did we end up in a given code path or method. For that we could use the IDE to show us all the references to any given variable, method and so on, but sometimes there's so many calls to what we want to trace, it becomes difficult to analyse.

This is when breakpoints and the `Call Stack` window come to place.

Once your code is stopped at any breakpoint, you should see at the bottom a window called `Call Stack`. Those items in the list are from top to bottom, the order of execution the code has taken until the line you put a breakpoint.

### Anything missing?

Should you have any questions, don't hesitate to ask questions at our discord. We'll be happy to help.