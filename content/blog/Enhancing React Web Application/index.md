---
title: 'Enhancing Your React Web Application From the Client Side'
date: "2021-01-04T07:26:03.284Z"
description: "A code-bite on how I was able to improve performance of my React web application from the client side."
categories: [javascript, react, web-development, webpack, performance]
comments: true
---

There are many things you could focus on when trying to enhance the performance of your web application. This article will introduce key points in which I was able to improve my React web application from the client side. Every application is different and has their own bottlenecks, limitations, and sets of users, but the following points are a good starting point! 

## Removing Unused Code

Software development can take awhile. Throughout that time you may accumulate a lot of technical debt in the form of unused JavaScript code, unused CSS, or even multiple imports of the same library! 

Wow, how does that happen? It happened when you use a library wrapping a third party library, and then the actual application references the third party library directly, thereby creating two references to the same library. A simple fix but a necessary one! We were able to save over 1MB by removing the old and outdated imports. 

### Researching Your Application Bundle Size

Before you make any changes, you should first research and analyze your web application. I recommend these two libraries to help understand your application better: [webpack-bundle-analyzer,](https://www.npmjs.com/package/webpack-bundle-analyzer) [source-map-explorer](https://www.npmjs.com/package/source-map-explorer), [Chrome Devtools (Performance Analyzer)](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance). 

### Shoutouts to Specific Libraries

**Lodash**

Another way you can accidentally introduce more bloat to your library is when you use a large library like Lodash. Generally, you would only use a few (or more!) functions from Lodash. However, if you import lodash incorrectly, it begins to import the whole library — a hefty size of 500KB!

We can and must make sure that our imported libraries are as lean as possible. Luckily there are a few plugins and ways to tree-shake unused code with libraries such as [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash) and [webpack-lodash-plugin](https://www.npmjs.com/package/lodash-webpack-plugin), lodash-es. Webpack v4 supposedly also supports lodash tree-shaking.

[Note](https://medium.com/making-internets/why-using-chain-is-a-mistake-9bc1f80d51ba): if you use _.chain, the method will import most of the Lodash library, so avoid it if possible!

**Moment.js**

Moment.js is a large and hefty library coming in at around 250KB. The way it is written makes it difficult for unused code to be tree-shaken. There is even a whole Github repository on why [You Don't Need Moment.js](https://github.com/you-dont-need/You-Dont-Need-Momentjs). So... well... do you? If you don't, there are many smaller sized libraries out there that may suit your needs well! 

These are just two specific libraries that often come up when you are looking to reduce bundle size. Perhaps the larger takeaway is to *be meticulous with introducing libraries and to make sure that they suit your needs well (performance and utility wise)*. 

## Moving Image Requests To Inlined Images

Our application had several small icons loaded from HTTP requests on every initial page load, taking approximately 0.5 seconds every time. This half a second is a lot for some tiny icons!

Because our icons were so small, and under 5KB each, we decided to inline them with the help of webpack, using the library [svg-inline-loader](https://v4.webpack.js.org/loaders/svg-inline-loader/).

This particular point goes in line with the larger idea that you must "*audit when and how assets are fetched.*" 

## Reducing React Re-Renders

Reduce DOM updates and re-calculations by making sure that your React code only re-renders when necessary. You can do things like move from Class Components to functional components to reduce your amount of code, use shouldComponentUpdate to fine tune your react renders, and more. 

## Optimize Your Webpack Bundles

On Chrome Devtools you can analyze your network chunks, and how your code is being loaded in. If your initial chunks of code are coming in and create a hilly mountain landscape, then that means that your chunks can be chunked in a more optimized way. Ideally, our chunks should look evenly sized throughout so that the page can become interactie at a faster time. 

## Conclusion

The above points were where I could find the most bang for my bunk in terms of development time and improving our application performance. Through this journey I realized that fine tuning performance in itself is a very long journey, and that you can get more and more detailed with improving the performance of your application. 

The above points are a good starting point  for improving your web applications performance on initial load. Another performance journey you could embark on is ensuring all [interactions of your applications are performant](https://web.dev/rail/). 

---

### Sources

When undergoing my own web application performance journey I underwent a fun and long googling session. These are the standouts to which I must give thanks to: [12 Tips To Improving Client Side Performance](https://medium.com/expedia-group-tech/12-tips-to-improve-client-side-page-performance-88c7bec27933), [Google Lighthouse](https://developers.google.com/web/tools/lighthouse), [SVG Inline or as HTTP Requests](https://stackoverflow.com/questions/23210126/inline-svg-vs-svg-file-performance), [Why Using _.chain is a Mistake](https://medium.com/bootstart/why-using-chain-is-a-mistake-9bc1f80d51ba), [Evaluate Web Performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance), and the [RAIL Model](https://web.dev/rail/).