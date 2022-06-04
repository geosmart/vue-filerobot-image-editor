# Filerobot Image Editor

![](https://scaleflex.airstore.io/filerobot/assets/filerobotimageeditor3_min.gif?sanitize=true)

## Requirements

- [Vue.js](http://vuejs.org/) >= 2

## Install

### CDN

```html

<script src="https://unpkg.com/@rotsen/vue-filerobot-image-editor"></script>
```

### NPM

```
$ npm install @rotsen/vue-filerobot-image-editor --save
or 
$ yarn @rotsen/vue-filerobot-image-editor

```

# Filerobot Image Editor

### Component

Then in your component:

```vue

<template>
    <div id="app">
        <img alt="Vue logo"
             src="./assets/logo.png"
             style="width:64px;height:64px"/>
        <img v-if="!openEditor" :src="url" @click="handleOpenEditor"/>
        <FilerobotImageEditor
            v-if="openEditor"
            :src="url"
            @modify="handleModify"
            @close="handleClose"
            @save="handleSave"
            @error="handleError"
            @beforeSave="onBeforeSave"
        />
    </div>
</template>
<script>
/* eslint-disable */
import FilerobotImageEditor from "./index";

export default {
    name: "App",
    components: {
        FilerobotImageEditor,
    },
    data() {
        return {
            url:
                "https://www.debian.org/Pics/debian-logo-1024x576.png",
            openEditor: false,
        };
    },
    mounted() {
    },
    methods: {
        handleModify(imgData) {
            console.info('imgData', imgData)
        },
        handleOpenEditor() {
            this.openEditor = true;
        },
        handleCloseEditor() {
            this.openEditor = false;
        },
        handleClose(status) {
            console.error('Close' + status)
            this.handleCloseEditor();
        },
        onBeforeSave(imageFileInfo) {
            console.error('imageFileInfo', imageFileInfo)
        },
        handleSave(editedImageObject, designState) {
            console.log("editedImageObject", editedImageObject)
            console.log("designState", designState)
            this.url = editedImageObject.imageCanvas.toDataURL();
            console.log('canvas data url', this.url)
            console.log('watermark', designState.annotations.watermark)
            //this.handleCloseEditor();
        },
        handleError(error) {
            this.handleCloseEditor();
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>

```

### Props

| Name                    | Type       | Description                                                                  |
| ----------------------- | ---------- | ---------------------------------------------------------------------------- |
| `config`                | `Object`   | All configuration of FilerobotImage Editor. **Default:
{}**                               |
| `src         `          | `String`   | Image url to edit . **Required** |

### Events

| Name                 | Description                                                                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `close`               | Fired when the editor is close                                                           |
| `error`               | Fired when error occurs                                                                   |
| `beforeSave`          | Event fired when click to Save of Download                                                |
| `save`                | Event fired when a dialog definition at the end of beforeSave                             |
| `modify`             | Event fired after any operation/transformation is applied on the image (ex. Add/change filter, resize the image...etc.). |

### Docs

```
Full docs at  [filerobot-image-editor](https://github.com/scaleflex/filerobot-image-editor)

```

## Build Setup

You can use [vue-cli](https://github.com/vuejs/vue-cli)  or [other vue templates](https://github.com/vuejs-templates)

## Created By

- [Nestor koueya](https://github.com/koueya)

Thanks to [contributers](./CONTRIBUTING.md)

## License

MIT
