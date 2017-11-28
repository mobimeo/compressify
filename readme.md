# Image-compression executable

Image compression executable to run as pre or post-commit. Compresses images in the same place, builds hash-manifest and stages changed images.

## Install

`npm install --save-dev https://github.com/moovel/web-compress-images-in-same-place.git`

## Usage

Image compression can run as standalone CLI command or used in combination with [husky](https://www.npmjs.com/package/husky) as pre-push. It will try to read the `--manifest` file and filter the already compressed images. The remaining images in the pipe will be compressed using [mozjpeg](https://github.com/mozilla/mozjpeg) and added to the stage. After compression takes place the hash manifest will be recreated, added to the stage and everything is committed.

```json
// package.json
{
  "scripts": {
    "prepush": "npm run compress",
     "compress": "compress-images-in-same-place --dest 'content' --src 'content/**/*.{jpg,jpeg,png}' --manifest 'image-manifest.json'"
  },
  "devDependencies": {
    "husky": "^0.14.3",
    "image-compression-executable": "git+https://github.com/moovel/web-compress-images-in-same-place.git"
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
