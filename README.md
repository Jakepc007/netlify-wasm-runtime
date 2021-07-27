This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/cassidoo/next-netlify-starter).

This project is aimed to demonstrate how to implement a Serverless Functions working with Webassembly in Netlify. The [main branch](https://github.com/second-state/netlify-wasm-runtime/tree/main) showcases an image processing function, and the [tensorflow branch](https://github.com/second-state/netlify-wasm-runtime/tree/tensorflow) showcases an AI inference function. Both written in simple Rust and runs in the [WasmEdge runtime](https://github.com/WasmEdge/WasmEdge) for WebAssembly.

## Overview

The Serverless Functions endpoint is located at `api/hello.js` to meet the requirement of Netlify, but not to the Next.js. So if you want to develop on you local machine, you should put it into `pages/api/` and make some change.

The only function in `api/hello.js` is classifying the object in a photo. It receives a jpg file and pass it as stdin stream to a spawned child process. The child process runs using the [wasmedge-tensorflow-lite](https://github.com/second-state/WasmEdge-tensorflow-tools) command.

File `api/functions/image-classification/src/main.rs` implements the tensorflow-based image recognition logic. You can build it with the Rust `cargo` command with the `-target wasm32-wasi --release` option to get the `classify.wasm` file.

We define custom build in `api/pre.sh` which is called in package.json to download the [WasmEdge command](https://github.com/WasmEdge/WasmEdge/releases/tag/0.8.2-rc.2).

![](/netlify-wasmedge-runtime.gif)


## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

To learn more about Serverless Functions in Netlify, take a look at the following resources:

- [Serverless Functions](https://docs.netlify.com/functions/overview/) - how to write your Serverless Functions.

## Deploy on Netlify

The easiest way to deploy your Next.js app is to use the [Netlify Platform](https://www.netlify.com/with/nextjs/).

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
