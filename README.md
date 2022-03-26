# glTF parser for Zig codebase

This project is a glTF 2.0 parser written in Zig, aiming to replace the use of some C/C++ libraries. 

It's not as complete as the glTF specification yet, but because it's straightforward to add
new parsing fields, the idea is to get new stuff incrementally and on-demand.

All glTF types are fully documented, so it comes nicely with IDE autocompletion, reducing 
back and forth with the [specification](https://www.khronos.org/registry/glTF/specs/2.0/glTF-2.0.html).

If you would like to contribute, don't hesitate! :)

## Examples

```zig
const std = @import("std");
const Gltf = @import("Gltf.zig");

const allocator = std.heap.page_allocator;
const print = std.debug.print;

pub fn main() void {
    const buffer = try std.fs.cwd().readFileAlloc(
        allocator,
        "test-samples/rigged_simple/RiggedSimple.gltf",
        512_000,
    );
    defer allocator.free(buf);

    var gltf = try Self.init(allocator, buf);
    defer gltf.deinit();

    for (gltf.nodes.items) |node| {
        const message =
            \\\ Node's name: {s}
            \\\ Children count: {}
            \\\ Have skin: {}
        ;

        print(message, .{
            node.name,
            node.children.items.len,
            node.skin != null,
        });
    }
}
```

## Features

- [x] glTF 2.0 json file
- [x] Scenes
- [x] Nodes
- [x] Meshes
- [x] Materials
- [x] Animations
- [x] Skins
- [ ] Lights
- [ ] Cameras
- [ ] Morth targets
- [ ] Extras data
- [ ] glTF writer
- [ ] glTF extensions

## Contributing to the project

Don’t be shy about shooting any questions you may have. If you are a beginner/junior, don’t hesitate, I will always encourage you. It’s a safe place here. Also, I would be very happy to receive any kind of pull requests, you will have (at least) some feedback/guidance rapidly.

Behind screens, there are human beings, living any sort of story. So be always kind and respectful, because we all sheer to learn new things.
