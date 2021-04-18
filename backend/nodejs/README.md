# NodeJS

## Core Concepts

Node.js is an **open-source and cross-platform JavaScript runtime environment.**                                                         `-> Node.js의 정의`

Node.js runs the **V8 JavaScript engine**, the core of Google Chrome, outside of the browser                                   `-> Node.js의 의의`

A Node.js app **runs in a single process, without creating a new thread** for every request. Node.js **provides a set of asynchronous I/O primitives in its standard library** that prevent JavaScript code from blocking and generally, libraries in Node.js are written using non-blocking paradigms, making blocking behavior the exception rather than the norm. When Node.js performs an I/O operation, like reading from the network, accessing a database or the filesystem, instead of blocking the thread and wasting CPU cycles waiting, Node.js will resume the operations when the response comes back. **This allows Node.js to handle thousands of concurrent connections with a single server without introducing the burden of managing thread concurrency, which could be a significant source of bugs.**  
`-> Node.js의 특징과 scalable한 이유`

Node.js has a **unique advantage because millions of frontend developers that write JavaScript for the browser are now able to write the server-side code in addition to the client-side code without the need to learn a completely different language**.                                                                                                                                          `->  Node.js가 부흥한 이유`

**In Node.js the new ECMAScript standards can be used without problems,** as you don't have to wait for all your users to update their browsers - you are **in charge of deciding which ECMAScript version to use by changing the Node.js version,** and you can also enable specific experimental features by running Node.js with flags.                                                                                                                                                                                   `-> V8 version 동기화와  ECMAScript`

Node.js **has a fantastic standard library**. Also, Node.js **has vast number of libraries**. [**npm**](https://www.npmjs.com/) with its simple structure helped the ecosystem of Node.js proliferate, and now the npm registry **hosts over 1,000,000 open source packages** you can freely use. Node.js is a low-level platform. In order to **make things easy and exciting for developers, thousands of libraries were built upon Node.js by the community.**                               `-> 유용한 standard library를 지원하며, 다양한 오픈소스 패키지나 프레임워크들이 존재`

### 

### Summury

* Chromium의 [**V8**](https://v8.dev/) 엔진을 기반으로 만들어짐
  * **can write Javascript code outside the browser**
* **non-blocking, lightweight, fast, robust and scalable framework**
* 비동기\(Asynchronous\)
* 이벤트 주도\(Event-driven\)
* Non-Blocking I/O

## Architecture

* **internal mechanics of the framework**
* single threaded, event loop based apparatus for achieving asynchronous behaviour

![https://www.simplilearn.com/understanding-node-js-architecture-article](../../.gitbook/assets/image%20%2877%29.png)

### Reference

{% embed url="https://nodejs.org/ko/" %}

{% embed url="https://nodejs.org/en/docs/guides/" %}

{% embed url="https://www.simplilearn.com/understanding-node-js-architecture-article" %}

{% embed url="https://scoutapm.com/blog/nodejs-architecture-and-12-best-practices-for-nodejs-development" %}





