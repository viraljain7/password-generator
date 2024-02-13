# React + Vite


# Final Screenshot Website Preview
![Screenshot (1)](https://github.com/viraljain7/password-generator/assets/88425229/39993166-af42-4e70-b42b-2fccc10d57de)

## UI/UX Template

```js
<div
  className="w-full max-w-md mx-auto shadow-md rounded-lg px-8 py-6
     my-8 text-orange-500 bg-gray-800 mt-40"
>
  <h1 className="text-white text-center text-2xl my-3">Password Generator</h1>
  <div className="flex shadow rounded-lg overflow-hidden mb-4">
    <input
      type="text"
      className="outline-none w-full py-1 px-3 rounded-md text-black"
      placeholder="Password"
      readOnly
    />

    <button className="bg-gray-600 px-2 py-2 rounded-lg text-white mx-1">
      Generate
    </button>
    <button className="px-3 py-0.5 bg-blue-700 text-white mx-2 rounded-md shrink-0 ">
      Copy
    </button>
  </div>
  <div className="flex text-sm gap-x-2">
    <div className="flex items-center gap-x-1 ">
      <input
        type="range"
        min={6}
        max={15}
        className="cursor-pointer appearance-none h-1 rounded-lg bg-black outline-none"
      />
      <label>length : {length}</label>
    </div>
    <div className="flex items-center gap-x-1 ">
      <input type="checkbox" id="numberInput" />
      <label htmlFor="numberInput">Numbers</label>
    </div>
    <div className="flex items-center gap-x-1 ">
      <input type="checkbox" id="numberInput" />
      <label htmlFor="numberInput">Characters</label>
    </div>
  </div>
</div>
```

## Hooks to import

```js
import { useCallback, useState, useEffect, useRef } from "react";
```

## variable & useRef

```js
// State variables
const [length, setLength] = useState(8);
const [numAllowed, setNumAllowed] = useState(false);
const [charAllowed, setCharAllowed] = useState(false);
const [password, setPassword] = useState("");

// useRef hook
const passwordRef = useRef(null);
```

## usecallback and passGenerator logic

```js
//useCallback- store in memory for short time
const passwordGenerator = useCallback(() => {
  let pass = "";
  let str = "QWERTYUIOPASDFGHJKLZXCVBNMqwertyuiopasdfghjklzxcvbnm";

  if (isCharAllow) {
    str += "!@#$%^&*()";
  }
  if (isNumAllow) {
    str += "0123456789";
  }

  for (let i = 1; i < length; i++) {
    let char = Math.floor(Math.random() * str.length + 1);
    pass += str.charAt(char);
  }

  setPassword(pass);
}, [isCharAllow, isNumAllow, length, setPassword]);
```

## useeffect

```js
//useffect- optimize the algo if any parameter change
useEffect(() => {
  passwordGenerator();
}, [length, isNumAllow, isCharAllow, passwordGenerator]);

const copyToClipBoard = useCallback(() => {
  passRef.current?.select();
  passRef.current?.setSelectionRange(0, 15);
  window.navigator.clipboard.writeText(password);
}, [password]);
```

## copy to clipboard logic

```js
const copyToClipBoard = useCallback(() => {
  passRef.current?.select();
  passRef.current?.setSelectionRange(0, 15);
  window.navigator.clipboard.writeText(password);
}, [password]);
```

# Code:

```js
import { useCallback, useState, useEffect, useRef } from "react";
import "./App.css";

function App() {
  const [isNumAllow, setIsNumAllow] = useState(false);
  const [isCharAllow, setIsCharAllow] = useState(false);
  const [length, setLength] = useState(8);
  const [password, setPassword] = useState("");

  // useRef
  const passRef = useRef(null);

  //useCallback- store in memory for short time
  const passwordGenerator = useCallback(() => {
    let pass = "";
    let str = "QWERTYUIOPASDFGHJKLZXCVBNMqwertyuiopasdfghjklzxcvbnm";

    if (isCharAllow) {
      str += "!@#$%^&*()";
    }
    if (isNumAllow) {
      str += "0123456789";
    }

    for (let i = 1; i < length; i++) {
      let char = Math.floor(Math.random() * str.length + 1);
      pass += str.charAt(char);
    }

    setPassword(pass);
  }, [isCharAllow, isNumAllow, length, setPassword]);

  //useffect- optimize the algo if any parameter change

  useEffect(() => {
    passwordGenerator();
  }, [length, isNumAllow, isCharAllow, passwordGenerator]);

  const copyToClipBoard = useCallback(() => {
    passRef.current?.select();
    passRef.current?.setSelectionRange(0, 15);
    window.navigator.clipboard.writeText(password);
  }, [password]);

  return (
    <>
      <div
        className="w-full max-w-md mx-auto shadow-md rounded-lg px-8 py-6
     my-8 text-orange-500 bg-gray-800 mt-40"
      >
        <h1 className="text-white text-center text-2xl my-3">
          Password Generator
        </h1>
        <div className="flex shadow rounded-lg overflow-hidden mb-4">
          <input
            type="text"
            className="outline-none w-full py-1 px-3 rounded-md text-black"
            placeholder="Password"
            value={password}
            readOnly
            ref={passRef}
          />

          <button
            className="bg-gray-600 px-2 py-2 rounded-lg text-white mx-1"
            onClick={passwordGenerator}
          >
            Generate
          </button>
          <button
            className="px-3 py-0.5 bg-blue-700 text-white mx-2 rounded-md shrink-0 "
            onClick={copyToClipBoard}
          >
            Copy
          </button>
        </div>
        <div className="flex text-sm gap-x-2">
          <div className="flex items-center gap-x-1 ">
            <input
              type="range"
              min={6}
              max={15}
              value={length}
              className="cursor-pointer appearance-none h-1 rounded-lg bg-black outline-none"
              onChange={(e) => {
                setLength(e.target.value);
              }}
            />![Screenshot (1)](https://github.com/viraljain7/password-generator/assets/88425229/f6de977b-c2c7-4744-8902-a4a5e58c1c79)

            <label>length : {length}</label>
          </div>
          <div className="flex items-center gap-x-1 ">
            <input
              type="checkbox"
              id="numberInput"
              onChange={() => {
                setIsNumAllow((prev) => !prev);
              }}
            />
            <label htmlFor="numberInput">Numbers</label>
          </div>
          <div className="flex items-center gap-x-1 ">
            <input
              type="checkbox"
              id="numberInput"
              onChange={() => {
                setIsCharAllow((prev) => !prev);
              }}
            />
            <label htmlFor="numberInput">Characters</label>
          </div>
        </div>
      </div>
    </>
  );
}

export default App;
```
