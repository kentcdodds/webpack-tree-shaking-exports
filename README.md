# webpack-tree-shaking-exports

This just shows that webpack is able to tree-shake exports from imports. Pretty neat.

You can either just look at the `bundle.js` and `bundle.prod.js` files in here, or you can
clone and build it yourself so you can mess around with things. Here's some details:

1. `index.js` is our entry
2. `bundle.js` is our webpack built file
3. `bundle.prod.js` is our webpack built file with `-p` flag (UglifyJS enabled)
4. `main.js` imports A, B, and C.
5. `A.js`, `B.js`, and `C.js` each have a single named export of the string `'A'`, `'B'`, and `'C'` respectively.

```
git clone https://github.com/kentcdodds/webpack-tree-shaking-exports.git
yarn
yarn run build
yarn run build:prod
```

Run the `build` script and open up the `bundle.js` to see how webpack will omit the exports in the `main.js`

Then run the `build:prod` script and open up the `bundle.prod-formatted.js` and you'll see that there are no occurrences of the strings "B" or "C" in the output. They were tree-shaken out!

**What's happening?**

When you run the `build` webpack looks at the import statements and marks each as used/unused (my guess is that all start as unused and as webpack resolves `imports` it marks them as used).
You'll notice in the `bundle.js` file that there's a comment indicating that there are some unused exports for the B and C exports. Those do NOT get the fancy `__webpack_require__.d(__webpack_exports__` stuff.
If you look at the code, you'll notice that `const B = 'B'` and `const C = 'C'` are unused variables. So if you were to uglify this file, those variables would be removed!
And this is exactly what happens. If you look in the `bundle.prod-formatted.js` file, you'll not find any references to those in the output. The entire module has been removed by UglifyJS. The unused variables are removed, Tree shaking FTW!

