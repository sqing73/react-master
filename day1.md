## Build React source code
clone source code

`git clone https://github.com/facebook/react.git`

install dependcies

`yarn`

build react, react-dom, react-dom-client, scheduler.

* client is necessary, because since **React** 18, `createRoot` from the client is used to create the app (💡 to verity )

`yarn build react/index,react/jsx,react-dom/index,react-dom/client,scheduler --type=NODE`

create links for the packages built

```
cd build/oss-stable
cd react
yarn link
```
repeat for react-dom, scheduler

create a new **React** applicaiton and link the packages built from source
```
yarn link react
yarn link react-dom
yarn link scheduler
```

Cha-ching...

Print something in log in `react-jsx-dev-runtime.development.js` and start the application, you should now see the lines printed console. 🚀🚀🚀
