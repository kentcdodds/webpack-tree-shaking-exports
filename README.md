# webpack-tree-shaking-exports

This just shows that webpack is able to tree-shake exports from imports. Pretty neat

```
git clone https://github.com/kentcdodds/webpack-tree-shaking-exports.git
yarn
yarn run build
yarn run build:prod
```

Run the `build` script and open up the `bundle.js` to see how webpack will omit the exports in the `main.js`

Then run the `build:prod` script and open up the `bundle.prod.js` and you'll see that there are no occurrences of the strings "B" or "C" in the output. They were tree-shaken out!

