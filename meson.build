project('hello')

generated_protos = generator(
  find_program('sh'),
  output: ['@BASENAME@_modified.proto'],
  arguments: [
    '-c',
    'sed "s/package internal/package whatever/" "$0" > "$1"',
    '@INPUT@', '@OUTPUT@'
  ],
).process([
  'proto/bar/bar.proto',
  'proto/foo/foo.proto',
])

proto_srcs = generator(
  find_program('cp'),
  output: ['@PLAINNAME@.cc'],
  arguments: ['@INPUT@', '@OUTPUT@'],
).process(generated_protos)

custom_target(
  'hello',
  build_by_default: true,
  input: proto_srcs,
  output: 'hello.txt',
  command: ['touch', '@OUTPUT@'],
)

