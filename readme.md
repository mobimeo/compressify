# compressify

Image compression executable to run as pre or post-commit. Compresses images in the same place, builds hash-manifest and stages changed images.

## Install

`npm install --save-dev https://github.com/moovel/compressify.git`

## Usage

Image compression can run as standalone CLI command or used in combination with [husky](https://www.npmjs.com/package/husky) as pre-commit. It will try to read the `--manifest` file and filter the already compressed images. The remaining images in the pipe will be compressed using [mozjpeg](https://github.com/mozilla/mozjpeg) and added to the stage. After compression takes place the hash manifest will be recreated, added to the stage and everything is committed.

```json
// package.json
{
  "scripts": {
    "precommit": "npm run compress",
    "compress": "compressify --dest 'content' --src 'content/**/*.{jpg,jpeg,png}' --manifest 'image-manifest.json'"
  },
  "devDependencies": {
    "husky": "^0.14.3",
    "compressify": "git+https://github.com/moovel/compressify.git"
  }
}
```

## API

| `--src`  |                                 |
| -------- | ------------------------------- |
| type     | `string`                        |
| required | `true`                          |
| desc     | source path of images           |
| example  | `'content/**/*.{jpg,jpeg,png}'` |

| `--dest` |                            |
| -------- | -------------------------- |
| type     | `string`                   |
| required | `true`                     |
| desc     | destination path of images |
| example  | `'content'`                |

| `--manifest` |                             |
| ------------ | --------------------------- |
| type         | `string`                    |
| required     | `true`                      |
| desc         | desc: path to hash manifest |
| example      | `'image-manifest.json'`     |

| `--gitadd` |                                              |
| ---------- | -------------------------------------------- |
| type       | `bool`                                       |
| default    | `true`                                       |
| required   | `false`                                      |
| desc       | if images should be staged after compression |
| example    | `false`                                      |
