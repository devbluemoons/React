## Moment.js
  
```sh
yarn add moment --save
## or
npm install moment --save
```
  
###### `sampe.js` file
```js
import moment from "moment";

const today = moment().format("YYYYMMDD"); 

const currentDate = "20201010"
const convertedDate = moment(currentDate).format("YYYY년 MM월 DD일");
```
