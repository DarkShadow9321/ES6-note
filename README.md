```css
Async = 非同步 、 sync = 同步
Async 執行後會馬上會下一個指令，例如:click, AJAX, Setlnterval
解決方法: callback,promises, async await
舉例來說callback的行為當典籍按鈕後，會執行某個function。
Promises 是屬於ES6的一部分，會return resolve or reject，Promise物件一實體化後會固定住狀態，不是顯示"已實現"就是"已拒絕"
sync則需要等第一個執行完後才可執行下一個
```
```js
function logWord(word) {
    setTimeout(function () {
        console.log(word)
    }, Math.floor(Math.random() * 100) + 1
        // return value between 1 ~ 100
    )
}
function logAll() {
    logWord("A")
    logWord("B")
    logWord("C")
}
logAll()
這樣輸出的結果為隨機，輸出不會固定
// Callbacks
function logWord(word, callback) {
    setTimeout(function () {
        console.log(word)
        callback()
    }), Math.floor(Math.random() * 100) + 1
}
function logAll() {
    logWord("A", function () {
        logWord("B", function () {
            logWord("C", function () { })
        })
    })
}
logAll()
```
用callback的方式寫雖然可以固定輸出結果，但如果在其中一部份出錯，則會很難找出錯誤。
```js
// Promises
function logWord(word) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log(word)
            resolve()
        }, Math.floor(Math.random() * 100) + 1)
    })
}
function logAll() {
    logWord('A')
        .then(function () {
            return logWord('B')
        })
        .then(function () {
            return logWord('C')
        })
}
logAll()
//Promises的做法則較為整齊也較容易理解。
function logAll() {
    logWord('A')
        .then(() => logWord('B'))
        .then(() => logWord('C'))
}
```
```css
Async await:
Promise的簡寫(底層還是promise)
async宣告被定義為非同步函式，且會回傳一個Promise
await等待一個promise的回傳(只能用在async function裡面)
```
```js
function logWord(word) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log(word)
            resolve()
        }, Math.floor(Math.random() * 100) + 1)
    })
}
// function logAll() {
// logWord('A')
// .then(function() {
// return logWord('B')
// })
// .then(function() {
// return logWord('C')
// })
// }
async function logAll() {
    await logWord('A')
    await logWord('B')
    await logWord('C')
}
logAll()
```
```js
抓取api
async function fetchData(){
    let res = await fetch('https://jsonplaceholder.typicode.com/posts/1')
    let data = await res.json()
    console.log(data)
}
fetchData()
Async await錯誤處理:
async function fetchDataWithError(){
    try{
        let res = await fetch('https://jsonplaceholder.typicode.com/posts/1')
    let data = await res.json()
    console.log(data)
    } catch(e){
      console.log("error",e)
    }
}
fetchDataWithError()
```
```css
從上面可以了解到Async await 比 Promise then 更簡單也更簡潔，
參考資料:
https://www.youtube.com/watch?v=UGf0fGMxDgE
https://gist.github.com/kuanhsuh/7a336abbcdc16fdb9545ede5e3b70026
https://www.youtube.com/watch?v=WEITXikGy6k
https://gist.github.com/kuanhsuh/5dfb213b38d783b68fac88cbfb596196

```
