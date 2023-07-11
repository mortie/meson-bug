# Meson bug?

This seems to be a bug in meson.

The [meson.build](meson.build) defines two levels of generators.

The first processes a list of .proto files,
and uses `sed` to replace `package internal` with `package whatever`.

The second processes the output of the first generator,
and uses `cp` to create a copy with `.cc` appended to the name.

My understanding is that this should work, and meson seems to agree;
`meson setup build` finishes with no error.
However, the `build.ninja` file it generates is broken.
Running `ninja -C build` makes ninja fail with this error:

    ninja: error: 'bar_modified.proto', needed by 'hello.txt.p/bar_modified.proto.cc',
    missing and no known rule to make it
