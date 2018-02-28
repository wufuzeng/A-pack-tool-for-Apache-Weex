## How to devloping web plugin

Open the template project generated by the `weex plugin create` command.

### Commands

`npm start` -- It will run the debug server, you can open the browser, visit `http://localhost:12580/` to see the plug-in presentation.

`npm run build`  -- Package the JS file.

`npm run dev:examples:web` -- Run the compile task on the watch mode.

`npm run build:examples:web` -- Package the examples on `example` folder.

### Develop

Web Plugin is divided into component development and module development
- The components are generally used for the business view logic
- The module is typically used for calling the Native API interface

** Component examples **

```
const _css = `
body > .weex-div {
  min-height: 100%;
}
`
function getDiv (weex) {
  const {
    extractComponentStyle,
    trimTextVNodes
  } = weex
  return {
    name: 'weex-div',
    render (createElement) {
      return createElement('html:div', {
        attrs: { 'weex-type': 'div' },
        staticClass: 'weex-div weex-ct',
        staticStyle: extractComponentStyle(this)
      }, trimTextVNodes(this.$slots.default))
    },
    _css
  }
}
function init(weex) {
   const div = getDiv(weex)
   weex.registerComponent('div', div)
}
export default {
  init:init
}
```

** Modules example **

```
const weexalert = {
  show() {
      weexalert("module WeexPluginDemo is created sucessfully ")
  }
};
const meta = {
   WeexPluginDemo: [{
    name: 'show',
    args: []
  }]
};
function init(weex) {
  weex.registerModule('weexalert', weexalert, meta);
}
export default {
  init:init
}
```
More detail you can see [extend-web-render](http://weex.apache.org/guide/extend-web-render.html).

### Test

You can run `npm start` and  visit `http://localhost:12580/` to see the plug-in presentation.