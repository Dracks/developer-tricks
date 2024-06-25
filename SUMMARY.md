# Tips and Tricks developing
My intention is to collect some of the tips and tricks I use/search for developing

## Swift

### Build and run on change

When developing server apps in nodejs, is common to have some command watch to build and run the server on any change, this is not possible on swift. But I found the solution using entr. 

Create some watch.sh file (or similar) and put this into the contents:
```sh
find . -name "*.swift" | entr -s "swift build"
```

I've got pending to improve it, as currently doesn't support change adding new files or deleting them. 


### Swift exceptions

This I used for the moment in a godot project, the idea is to make easy to work with exceptions with your own exception, thanks to godot, we can catch the line and the file in which a exception is created, the following classes are used: 

```swift
import SwiftGodot

enum ExceptionCode {
    case E1000
}

class Exception {
    var code: ExceptionCode
    var msg: String
    var ctx: [String:Any]
    var file: StaticString
    var line: UInt

    init(_ code: ExceptionCode, msg: String, ctx: [String:Any] = [:], file: StaticString = #file, line: UInt = #line) {
        self.code = code
        self.msg = msg
        self.ctx = ctx
        self.file = file
        self.line = line
    }

    func toString()->String {
        return "\(code): \(self.msg) (\(file):\(line))"
    }
}
```