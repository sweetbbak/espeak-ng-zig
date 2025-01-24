The [rhasspy/espeak-ng](https://github.com/rhasspy/espeak-ng) library packaged for the Zig build system.

This build doesn't compile any of the async, audio or ucd tools and features.
It is mainly used for phonemizing text.

# Changes in Fork

Add espeak_TextToPhonemesWithTerminator function that allows getting phonemes with punctuation type back (see python_test.py)

add to your project:

```sh
zig fetch --save https://github.com/sweetbbak/espeak-ng-zig/archive/refs/heads/main.zip
```

```zig
    const espeak = b.dependency("espeak", .{
        .target = target,
        .optimize = optimize,
        .strip = true,
        .pie = true,
    });

    // link with the output artifact
    exe.linkLibrary(espeak.artifact("espeak-ng"));

    // allow the headers to be included in your project
    const espeak_include = espeak.path("include");
    exe.addIncludePath(espeak_include);
```

import in your executable:

```zig
// provides  encoding.h   espeak_ng.h   speak_lib.h
const c = @cImport({
    @cInclude("speak_lib.h");
});
```
