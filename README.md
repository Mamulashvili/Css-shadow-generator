# box-shadow-generator

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
## Custom v-directives
- boxShadow
- boxColor
- boxBorderRadius

```js
v-box-shadow:[shadowColor]="{
  shadowDirection,
  horizontalLength,
  verticalLength,
  blurRadius,
  spreadRadius,
}"
```

``` js
 v-box-color="boxColor"
 v-box-border-radius="borderRadius"
```

## Reusable components
- BaseColorInput
- BaseRangeInput
- BaseSwitch
- BoxShadow (main screen)
