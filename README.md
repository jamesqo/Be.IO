# Be.IO

[![Build Status](https://travis-ci.org/jamesqo/Be.IO.svg?branch=master)](https://travis-ci.org/jamesqo/Be.IO) [![AppVeyor](https://ci.appveyor.com/api/projects/status/github/jamesqo/Be.IO?branch=master&svg=true)](https://ci.appveyor.com/project/jamesqo/be-io)

Be.IO is a fast big-endian implementation of .NET's BinaryReader and BinaryWriter.

## Installation

    Install-Package Be.IO

## Supported Platforms

Just about every platform is supported, including:

- .NET Framework 4.5+
- Windows 10 Universal apps
- Portable Class Libraries
- ASP.NET Core
- Xamarin.iOS
- Xamarin.Android
- Mono (Mac/Linux)
- Windows 8.1 and 8.0
- Windows Phone 8.1
- Silverlight

## Getting Started

First, add this using statement at the top of your file:

```csharp
using Be.IO;
```

After that, you can use `BeBinaryWriter` and `BeBinaryReader` the same way you would use a regular binary reader/writer. Example:

```csharp
using (var file = File.Open("foo.txt", FileMode.Create))
{
    var writer = new BeBinaryWriter(file);
    writer.Write(0x1357);
    writer.Write(0xDEADBEEF);
    writer.Write((long)9999999);
    
    var reader = new BeBinaryReader(file);
    short s = reader.ReadInt16();
    int i = reader.ReadInt32();
    long l = reader.ReadInt64();
}
```

## WARNING!

Character-based methods like `ReadString` still read characters in little-endian. This is because the `Encoding` you pass into the stream reader/writer is responsible for converting characters to bytes and vice versa, so it gets to choose which endian to use. If you need to read/write in an encoding that is endian-sensitive (like UTF-16), you'll have to find a big-endian version of that encoding.

## License?

Be.IO is licensed under the [BSD simplified license](license.bsd).
